# 内容

`RACSubject` 是 ReactiveCocoa 框架中的一个核心类，常用于 **手动控制事件的发送和处理**。它作为 **信号（Signal）和订阅者（Subscriber）** 的桥梁，允许开发者通过手动发送事件来控制信号流，同时允许多个订阅者接收事件。

#### `RACSubject` 的主要特点

1. **既是信号又是订阅者**：`RACSubject` 既能订阅其他信号，也能作为一个信号被订阅。这种设计让它可以在处理事件的同时，自身也能接收事件。
2. **手动控制事件发送**：通过 `sendNext:`, `sendError:`, 和 `sendCompleted` 这三个方法来发送不同类型的事件。
3. **多播特性**：支持多个订阅者共同接收同一个信号的事件，适合需要广播同一事件给多个观察者的场景。
4. **热信号**：事件发送后，不会缓存给后来的订阅者，这意味着新的订阅者只能接收其订阅后的事件。

#### `RACSubject` 的常用方法

* **`sendNext:`**：发送一个 `next` 事件，通常携带一个值，所有的订阅者会收到此事件。
* **`sendError:`**：发送一个错误事件，传递一个 `NSError` 对象给所有订阅者，之后会结束信号。
* **`sendCompleted`**：发送一个完成事件，告知所有订阅者信号已经完成，之后信号将不再发送事件。

#### 使用示例

**1. 基本使用**

创建一个 `RACSubject` 并发送一个简单事件：

```objc
// 创建一个 RACSubject
RACSubject *subject = [RACSubject subject];

// 订阅信号
[subject subscribeNext:^(id  _Nullable x) {
    NSLog(@"Received value: %@", x);
}];

// 发送事件
[subject sendNext:@"Hello, RACSubject!"];
```

输出：

```
Received value: Hello, RACSubject!
```

在这个例子中，`subject` 作为信号被订阅，订阅者会在事件发送时收到 `"Hello, RACSubject!"`。

**2. 多个订阅者**

`RACSubject` 支持多个订阅者，每个订阅者都会收到相同的事件：

```objc
RACSubject *subject = [RACSubject subject];

// 订阅者 1
[subject subscribeNext:^(id x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];

// 订阅者 2
[subject subscribeNext:^(id x) {
    NSLog(@"Subscriber 2 received: %@", x);
}];

// 发送事件
[subject sendNext:@"Event for both subscribers"];
```

输出：

```
Subscriber 1 received: Event for both subscribers
Subscriber 2 received: Event for both subscribers
```

**3. 用于桥接非响应式事件**

`RACSubject` 可以将传统的回调模式转换成响应式信号流。例如，将按钮点击事件转成信号：

```objc
@interface MyViewController : UIViewController
@property (nonatomic, strong) RACSubject *buttonClickSubject;
@end

@implementation MyViewController

- (instancetype)init {
    self = [super init];
    if (self) {
        // 初始化 RACSubject
        self.buttonClickSubject = [RACSubject subject];
    }
    return self;
}

// 按钮点击事件
- (void)buttonClicked {
    // 手动发送事件
    [self.buttonClickSubject sendNext:@"Button clicked"];
}

@end

// 其他类中订阅此事件
MyViewController *vc = [[MyViewController alloc] init];
[vc.buttonClickSubject subscribeNext:^(id x) {
    NSLog(@"Received button click event: %@", x);
}];

// 模拟按钮点击
[vc buttonClicked];
```

输出：

```
Received button click event: Button clicked
```

#### `RACSubject` 和 `RACReplaySubject` 的区别

1. **`RACSubject`**：不缓存发送的事件，只有当前的订阅者可以接收到事件。
2. **`RACReplaySubject`**：会缓存一定数量的事件，新订阅者可以接收之前缓存的事件。

如果希望新的订阅者能够接收到之前发送的事件，使用 `RACReplaySubject` 更合适。

#### 适用场景

* **桥接传统回调**：将非响应式的事件（如代理、回调等）转换成响应式信号。
* **广播事件**：需要向多个订阅者发送相同事件时，`RACSubject` 可以作为广播工具。
* **手动控制事件发送**：适用于需要手动触发事件的场景。

#### 总结

`RACSubject` 是 ReactiveCocoa 中灵活、常用的信号类型之一。它结合了信号和订阅者的特点，适合用于需要手动控制事件、将传统回调桥接成信号流的场景，在响应式编程中提升代码的简洁性和可读性。
