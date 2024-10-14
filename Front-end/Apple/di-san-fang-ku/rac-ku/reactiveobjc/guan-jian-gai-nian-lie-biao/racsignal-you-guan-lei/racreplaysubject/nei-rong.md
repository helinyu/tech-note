# 内容

`RACReplaySubject` 是 ReactiveCocoa 中的一种 **特殊的热信号**，它与 `RACSubject` 相似，但具有 **事件缓存功能**。它允许将历史事件缓存下来，新订阅者可以接收到之前的事件，尤其适合在需要保留和重放事件的场景中使用。

#### `RACReplaySubject` 的特点

1. **事件缓存**：`RACReplaySubject` 会将发送的事件存储起来，新订阅者可以收到已缓存的历史事件。可以通过设置缓存数量来控制保留多少个事件。
2. **热信号**：`RACReplaySubject` 在被创建和触发后就立即发送事件，不需要等待订阅者。
3. **多播特性**：`RACReplaySubject` 支持多个订阅者，所有订阅者会收到相同的事件。

#### `RACReplaySubject` 的常用方法

与 `RACSubject` 类似，`RACReplaySubject` 也有如下方法用于发送事件：

* **`sendNext:`**：发送一个 `next` 事件。
* **`sendError:`**：发送一个错误事件，并结束信号。
* **`sendCompleted`**：发送完成事件，通知所有订阅者信号结束。

#### 创建和使用示例

**1. 基本使用**

创建一个 `RACReplaySubject`，发送事件并进行订阅：

```objc
// 创建一个 RACReplaySubject
RACReplaySubject *replaySubject = [RACReplaySubject subject];

// 发送事件
[replaySubject sendNext:@"Event 1"];
[replaySubject sendNext:@"Event 2"];

// 订阅者 1
[replaySubject subscribeNext:^(id  _Nullable x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];
```

输出：

```
Subscriber 1 received: Event 1
Subscriber 1 received: Event 2
```

在这个例子中，`replaySubject` 在订阅之前就发送了 `"Event 1"` 和 `"Event 2"`。当订阅者 1 订阅时，立即收到了这些历史事件。

**2. 多个订阅者的情况下重放事件**

每个新订阅者都会接收到所有已缓存的事件：

```objc
// 创建一个 RACReplaySubject
RACReplaySubject *replaySubject = [RACReplaySubject subject];

// 发送事件
[replaySubject sendNext:@"Event 1"];
[replaySubject sendNext:@"Event 2"];

// 第一个订阅者
[replaySubject subscribeNext:^(id x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];

// 发送新的事件
[replaySubject sendNext:@"Event 3"];

// 第二个订阅者
[replaySubject subscribeNext:^(id x) {
    NSLog(@"Subscriber 2 received: %@", x);
}];
```

输出：

```
Subscriber 1 received: Event 1
Subscriber 1 received: Event 2
Subscriber 1 received: Event 3
Subscriber 2 received: Event 1
Subscriber 2 received: Event 2
Subscriber 2 received: Event 3
```

在这个例子中，第一个订阅者接收到所有事件，包括 `"Event 3"`。第二个订阅者也接收到所有已缓存的事件，尽管在 `"Event 3"` 之后才订阅。

**3. 设置缓存大小**

可以指定 `RACReplaySubject` 缓存的事件数量：

```objc
// 创建一个只缓存最后一个事件的 RACReplaySubject
RACReplaySubject *replaySubject = [RACReplaySubject replaySubjectWithCapacity:1];

// 发送多个事件
[replaySubject sendNext:@"Event 1"];
[replaySubject sendNext:@"Event 2"];

// 订阅信号
[replaySubject subscribeNext:^(id x) {
    NSLog(@"Received: %@", x);
}];
```

输出：

```
Received: Event 2
```

因为缓存大小设置为 `1`，`replaySubject` 仅缓存最新的 `"Event 2"`，所以新订阅者只接收到 `"Event 2"`。

#### `RACReplaySubject` 和 `RACSubject` 的区别

* **缓存机制**：`RACReplaySubject` 会缓存历史事件，并在新的订阅者加入时重放这些事件；`RACSubject` 不缓存事件，只有当前订阅者可以接收到事件。
* **适用场景**：`RACReplaySubject` 适合需要保存事件状态并让新订阅者接收到历史事件的场景；而 `RACSubject` 更适合实时事件广播。

#### 适用场景

* **状态重放**：例如，网络请求成功后缓存数据并允许新加入的订阅者接收数据。
* **事件广播**：`RACReplaySubject` 适合用于在多处广播同样的事件或状态。
* **避免事件丢失**：使用缓存功能确保新订阅者能接收到之前的重要事件，不会因为订阅顺序不同而丢失数据。

#### 总结

`RACReplaySubject` 是 ReactiveCocoa 中重要的信号类型之一，它通过缓存事件并重放给新订阅者，能解决一些常见的状态保留问题。在需要保证事件不丢失或新订阅者能接收到过去事件的场景中，它是一个非常有用的工具。
