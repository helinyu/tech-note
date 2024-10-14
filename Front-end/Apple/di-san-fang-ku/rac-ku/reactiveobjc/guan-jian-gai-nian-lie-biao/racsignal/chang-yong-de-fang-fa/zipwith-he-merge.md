# zipWith 和merge

`merge:` 和 `zipWith:` 是 ReactiveCocoa 中 `RACSignal` 提供的两种信号组合方法。它们在合并信号的方式和结果上有所不同。下面是它们之间的关系与区别：

#### 1. **merge:**

* **定义**：`merge:` 方法用于将多个信号合并成一个信号。当任何一个合并的信号发出一个值时，合并信号就会立即发出该值。
* **行为**：
  * 如果有多个信号同时发出值，合并信号会接收到每一个信号发出的值。
  * 每个发出的值与时间无关，直接传递。
* **示例**：

```objc
RACSignal *signal1 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"来自信号 1"];
    return nil;
}];

RACSignal *signal2 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"来自信号 2"];
    return nil;
}];

RACSignal *mergedSignal = [signal1 merge:signal2];

[mergedSignal subscribeNext:^(id x) {
    NSLog(@"接收到: %@", x);
}];

// 输出:
// 接收到: 来自信号 1
// 接收到: 来自信号 2
```

#### 2. **zipWith:**

* **定义**：`zipWith:` 方法用于将多个信号组合成一个信号，只有在所有组合信号都发出值时，合并信号才会发出一个包含所有值的元组。
* **行为**：
  * 合并信号的输出依赖于所有输入信号的输出，并且每次只有当所有信号都有新值时，合并信号才会发出新值。
  * 输出的元组包含了所有信号的最新值。
* **示例**：

```objc
RACSignal *signal1 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"信号 1 的值"];
    return nil;
}];

RACSignal *signal2 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"信号 2 的值"];
    return nil;
}];

RACSignal *zippedSignal = [signal1 zipWith:signal2];

[zippedSignal subscribeNext:^(RACTuple *tuple) {
    NSLog(@"接收到: %@", tuple);
}];

// 输出:
// 接收到: (
//     "信号 1 的值",
//     "信号 2 的值"
// )
```

#### 总结

* **`merge:`**:
  * 当任意一个信号发出值时，合并信号就会立即发出该值。
  * 每个发出的值独立，不需要其他信号的配合。
* **`zipWith:`**:
  * 只有在所有信号都发出值时，合并信号才会发出一个新的元组。
  * 输出是所有信号最新值的组合，确保每个信号都要参与到输出中。

