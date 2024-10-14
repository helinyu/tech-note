# 热信号和冷信号

在 ReactiveCocoa 中，`RACSignal` 可以分为**热信号**（Hot Signals）和**冷信号**（Cold Signals），这两种信号在行为和使用场景上有明显的区别。

#### 冷信号（Cold Signals）

* **定义**：冷信号在创建时并不会发出任何值，只有在有订阅者订阅时，信号才会开始发出值。
* **特性**：
  * 每次订阅都会创建一个新的信号实例。
  * 每个订阅者都会接收到信号的独立副本，意味着每个订阅者都从信号的开始点接收值。
* **示例**：
  * `RACSignal.createSignal:` 创建的信号通常是冷信号，只有在订阅时才开始执行。

```objc
RACSignal *coldSignal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"Hello"];
    return nil;
}];

// 第一次订阅
[coldSignal subscribeNext:^(id x) {
    NSLog(@"Subscriber 1: %@", x); // 输出 "Hello"
}];

// 第二次订阅
[coldSignal subscribeNext:^(id x) {
    NSLog(@"Subscriber 2: %@", x); // 也会输出 "Hello"
}];
```

#### 热信号（Hot Signals）

* **定义**：热信号在创建时就会开始发出值，不依赖于订阅者的存在。
* **特性**：
  * 所有的订阅者共享同一个信号实例，意味着订阅者之间是相互独立的，但会接收到相同的事件。
  * 信号在订阅之前就可以开始发出值。
* **示例**：
  * 通过 `RACSubject` 或其他类似的方式创建的信号通常是热信号。

```objc
RACSubject *hotSignal = [RACSubject subject];

// 第一个订阅者
[hotSignal subscribeNext:^(id x) {
    NSLog(@"Subscriber 1: %@", x);
}];

// 发送值
[hotSignal sendNext:@"Hello"];

// 第二个订阅者
[hotSignal subscribeNext:^(id x) {
    NSLog(@"Subscriber 2: %@", x);
}];

// 发送另一个值
[hotSignal sendNext:@"World"];
```

在这个例子中，`Subscriber 1` 会接收到 `"Hello"和"world"`，而 `Subscriber 2` 则会接收到 `"World"`，但不会接收到 `"Hello"`，因为它在订阅时已经发出。

#### 总结

* **冷信号**：每个订阅者都接收到独立的事件流，信号在订阅时开始发出值。
* **热信号**：所有订阅者共享同一个事件流，信号在创建时开始发出值，不依赖于订阅者的存在。



