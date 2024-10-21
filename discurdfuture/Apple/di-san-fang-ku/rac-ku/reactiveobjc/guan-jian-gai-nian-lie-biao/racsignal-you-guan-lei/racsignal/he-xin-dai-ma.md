# 核心代码

```objective-c
 // 创建第一个信号
        RACSignal *signal1 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
            [subscriber sendNext:@"信号 1 的值"];
            [subscriber sendCompleted];
            return nil;
        }];

        // 创建第二个信号
        RACSignal *signal2 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
            [subscriber sendNext:@"信号 2 的值"];
            [subscriber sendCompleted];
            return nil;
        }];

        // 使用 zip 合并信号
        RACSignal *zippedSignal = [signal1 merge:signal2];
    
        [zippedSignal subscribeNext:^(RACTuple *tuple) {
            NSLog(@"接收到: %@", tuple);
        } error:^(NSError * _Nullable error) {
            NSLog(@"错误: %@", error);
        } completed:^{
            NSLog(@"所有信号都已完成.");
        }];

```



### 1、创建信号量

```
//RACSignal
+ (RACSignal *)createSignal:(RACDisposable * (^)(id<RACSubscriber> subscriber))didSubscribe {
	return [RACDynamicSignal createSignal:didSubscribe];
}

//RACDynamicSignal
+ (RACSignal *)createSignal:(RACDisposable * (^)(id<RACSubscriber> subscriber))didSubscribe {
	RACDynamicSignal *signal = [[self alloc] init];
	signal->_didSubscribe = [didSubscribe copy];
	return [signal setNameWithFormat:@"+createSignal:"]; // 
}

// RACStream
- (instancetype)setNameWithFormat:(NSString *)format, ... {
	if (getenv("RAC_DEBUG_SIGNAL_NAMES") == NULL) return self;

	NSCParameterAssert(format != nil);

	va_list args;
	va_start(args, format);

	NSString *str = [[NSString alloc] initWithFormat:format arguments:args];
	va_end(args);

	self.name = str;
	return self;
}
```

1、调用RACDynamicSignal 类方法创建信号

2、 拷贝订阅block到当前的属性中

3、给信号设置（流）名字



### 2、合并信号量

```
- (RACSignal *)merge:(RACSignal *)signal {
	return [[RACSignal
		merge:@[ self, signal ]]
		setNameWithFormat:@"[%@] -merge: %@", self.name, signal];
}

+ (RACSignal *)merge:(id<NSFastEnumeration>)signals {
	NSMutableArray *copiedSignals = [[NSMutableArray alloc] init];
	for (RACSignal *signal in signals) {
		[copiedSignals addObject:signal];
	}

	return [[[RACSignal
		createSignal:^ RACDisposable * (id<RACSubscriber> subscriber) {
			for (RACSignal *signal in copiedSignals) {
				[subscriber sendNext:signal];
			}

			[subscriber sendCompleted];
			return nil;
		}]
		flatten]
		setNameWithFormat:@"+merge: %@", copiedSignals];
}

// RACStream 合并信号
- (__kindof RACStream *)flatten {
	return [[self flattenMap:^(id value) {
		return value;
	}] setNameWithFormat:@"[%@] -flatten", self.name];
}

- (__kindof RACStream *)flattenMap:(__kindof RACStream * (^)(id value))block {
	Class class = self.class;

	return [[self bind:^{
		return ^(id value, BOOL *stop) {
			id stream = block(value) ?: [class empty];
			NSCAssert([stream isKindOfClass:RACStream.class], @"Value returned from -flattenMap: is not a stream: %@", stream);

			return stream;
		};
	}] setNameWithFormat:@"[%@] -flattenMap:", self.name];
}

```

1、调用颞部的合并方法

2、遍历数组，然后执行里面的block【block的执行有保存作用，后面调用到的时候在调用】

3、 flattern中合并的 ，使用了bind: 修改了信号，成为了一个新的信号



### 3、订阅信号量

```
- (RACDisposable *)subscribeNext:(void (^)(id x))nextBlock error:(void (^)(NSError *error))errorBlock completed:(void (^)(void))completedBlock {
	NSCParameterAssert(nextBlock != NULL);
	NSCParameterAssert(errorBlock != NULL);
	NSCParameterAssert(completedBlock != NULL);
	
	RACSubscriber *o = [RACSubscriber subscriberWithNext:nextBlock error:errorBlock completed:completedBlock];
	return [self subscribe:o];
}

// RACDynamicSignal
- (RACDisposable *)subscribe:(id<RACSubscriber>)subscriber {
	NSCParameterAssert(subscriber != nil);

	RACCompoundDisposable *disposable = [RACCompoundDisposable compoundDisposable];
	subscriber = [[RACPassthroughSubscriber alloc] initWithSubscriber:subscriber signal:self disposable:disposable];

	if (self.didSubscribe != NULL) {
		RACDisposable *schedulingDisposable = [RACScheduler.subscriptionScheduler schedule:^{
			RACDisposable *innerDisposable = self.didSubscribe(subscriber);
			[disposable addDisposable:innerDisposable];
		}];

		[disposable addDisposable:schedulingDisposable];
	}
	
	return disposable;
}

```

1、创建一个RACSubscriber对象（里面就是拷贝有关的block到对象属性中）

2、初始化一个RACPassthroughSubscriber 对象，

3、不为空，就调度执行订阅，调用schedule方法，执行里面的block

4、self.didSubscribe(subscriber) ，这个就是上面我们创建信号的时候保留的block

