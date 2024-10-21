# 热信号 vs 冷信号

在 **ReactiveObjC** 中，信号主要分为**热信号（Hot Signal）和冷信号（Cold Signal）**。下面将展示如何分别创建这两种信号。

#### 1. **热信号**

**热信号** 是在创建后立即开始发送事件的信号，所有的订阅者会接收到当前或未来的事件。**`RACSubject`** 和普通的 **`RACSignal`** 都是热信号的例子。

**使用 `RACSubject` 创建热信号：**

`RACSubject` 是一个典型的热信号，允许手动发送事件并允许多个订阅者订阅。

```objc
RACSubject *subject = [RACSubject subject];

// 第一个订阅者
[subject subscribeNext:^(id x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];

// 发送事件
[subject sendNext:@1];

// 第二个订阅者，此时只能接收之后的事件
[subject subscribeNext:^(id x) {
    NSLog(@"Subscriber 2 received: %@", x);
}];

// 发送新事件
[subject sendNext:@2];
```

**使用 `RACSignal` 创建热信号：**

`RACSignal` 本身也是热信号，当它被创建时会立即开始执行，并发送事件。多个订阅者可以同时接收事件流。

```objc
RACSignal *signal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@1];
    [subscriber sendCompleted];
    return nil;
}];

// 订阅信号
[signal subscribeNext:^(id x) {
    NSLog(@"First subscriber received: %@", x);
}];

// 这里信号已经发送完毕，所以第二个订阅者不会收到任何事件
[signal subscribeNext:^(id x) {
    NSLog(@"Second subscriber received: %@", x);
}];
```

在这个例子中，由于信号在创建时就发送了事件，所以只有第一个订阅者能接收到 `@1`，第二个订阅者没有机会接收任何事件。

#### 2. **冷信号**

**冷信号** 是指只有在订阅时才会生成并发送事件，每次订阅都会重新执行信号的生成逻辑。这种模式可以保证每个订阅者都接收到相同的事件序列。

在 **ReactiveObjC** 中，**冷信号** 可以通过 `deferred` 或者自定义信号的方式来实现。虽然 `RACSignal` 默认是热信号，但通过手动控制其生成逻辑，可以模拟冷信号的行为。

**使用 `deferred` 创建冷信号：**

`RACSignal` 的 `deferred` 方法允许你延迟信号的创建，直到每次订阅时才生成事件流。

```objc
RACSignal *coldSignal = [RACSignal deferred:^RACSignal *{
    return [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
        NSLog(@"Signal created");
        [subscriber sendNext:@1];
        [subscriber sendCompleted];
        return nil;
    }];
}];

// 订阅冷信号，每次订阅都会触发新的事件流
[coldSignal subscribeNext:^(id x) {
    NSLog(@"First subscriber received: %@", x);
}];

[coldSignal subscribeNext:^(id x) {
    NSLog(@"Second subscriber received: %@", x);
}];
```

**自定义冷信号：**

我们可以通过 `RACSignal` 的 `createSignal:` 方法手动实现冷信号的行为，每次订阅时重新生成事件流。

```objc
RACSignal *coldSignal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    NSLog(@"Cold signal generated");
    [subscriber sendNext:@1];
    [subscriber sendCompleted];
    return nil;
}];

// 订阅冷信号，每次都会重新生成事件流
[coldSignal subscribeNext:^(id x) {
    NSLog(@"First subscriber received: %@", x);
}];

[coldSignal subscribeNext:^(id x) {
    NSLog(@"Second subscriber received: %@", x);
}];
```

#### 总结

* **热信号**：可以通过 `RACSignal` 和 `RACSubject` 创建。它们在创建时就开始发送事件，多个订阅者会共享同一事件流。
  * `RACSubject` 是一个手动控制事件发送的热信号。
  * `RACSignal` 默认是热信号，订阅后立即发送事件。
* **冷信号**：可以通过 `deferred` 方法或自定义的方式创建。冷信号会在每次订阅时重新生成事件，多个订阅者不会共享同一个事件流，每个订阅者都会独立地收到完整的事件序列。
