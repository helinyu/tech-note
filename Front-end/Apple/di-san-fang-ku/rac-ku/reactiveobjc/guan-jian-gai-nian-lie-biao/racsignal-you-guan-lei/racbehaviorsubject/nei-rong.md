# 内容

`RACBehaviorSubject` 是 ReactiveCocoa 中的一种特殊类型的信号，具有 **只缓存最新事件** 的特点。它适合用于始终保持并提供最新状态的场景中，新订阅者会立即收到最后一个事件（如果有），并且可以继续接收后续的事件。

#### `RACBehaviorSubject` 的特点

1. **只缓存最新事件**：`RACBehaviorSubject` 只会缓存并保留最新的事件，新订阅者订阅时可以立即收到该事件。
2. **保证初始值**：创建时可以指定一个默认值，这个值会作为第一个事件发送给订阅者，直到发送了新的事件。
3. **热信号**：事件会被直接发送给当前的订阅者，而不是等待订阅者订阅后才执行。
4. **多播特性**：支持多个订阅者接收同一事件。

#### 创建和使用示例

**1. 基本使用**

创建一个 `RACBehaviorSubject`，设置初始值并进行订阅：

```objc
// 创建一个带初始值的 RACBehaviorSubject
RACBehaviorSubject *behaviorSubject = [RACBehaviorSubject behaviorSubjectWithDefaultValue:@"Initial Value"];

// 第一个订阅者
[behaviorSubject subscribeNext:^(id x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];

// 发送新事件
[behaviorSubject sendNext:@"Event 1"];
```

输出：

```
Subscriber 1 received: Initial Value
Subscriber 1 received: Event 1
```

在这个例子中，订阅者 1 在订阅时立即接收到初始值 `"Initial Value"`，并接着收到新事件 `"Event 1"`。

**2. 新的订阅者会收到最后发送的事件**

如果有新的订阅者加入，`RACBehaviorSubject` 会将最新的事件发送给该订阅者：

```objc
// 创建一个带初始值的 RACBehaviorSubject
RACBehaviorSubject *behaviorSubject = [RACBehaviorSubject behaviorSubjectWithDefaultValue:@"Initial Value"];

// 发送新事件
[behaviorSubject sendNext:@"Event 1"];

// 第一个订阅者
[behaviorSubject subscribeNext:^(id x) {
    NSLog(@"Subscriber 1 received: %@", x);
}];

// 发送新的事件
[behaviorSubject sendNext:@"Event 2"];

// 第二个订阅者
[behaviorSubject subscribeNext:^(id x) {
    NSLog(@"Subscriber 2 received: %@", x);
}];
```

输出：

```
Subscriber 1 received: Event 1
Subscriber 1 received: Event 2
Subscriber 2 received: Event 2
```

在这里，`Subscriber 1` 收到了 `"Event 1"` 和 `"Event 2"`。而 `Subscriber 2` 订阅时收到了最新的事件 `"Event 2"`。

**3. 用于状态保持的场景**

`RACBehaviorSubject` 非常适合用于状态保持的场景，通常在 UI 中用于保存某个控件的当前状态，并让新加入的观察者立即获取到当前状态：

```objc
// 假设我们有一个表示加载状态的 BehaviorSubject
RACBehaviorSubject *loadingStateSubject = [RACBehaviorSubject behaviorSubjectWithDefaultValue:@(NO)];

// 订阅以监听加载状态变化
[loadingStateSubject subscribeNext:^(NSNumber *isLoading) {
    if (isLoading.boolValue) {
        NSLog(@"Loading started");
    } else {
        NSLog(@"Loading ended");
    }
}];

// 开始加载
[loadingStateSubject sendNext:@(YES)];

// 停止加载
[loadingStateSubject sendNext:@(NO)];
```

输出：

```
Loading started
Loading ended
```

#### `RACBehaviorSubject` 与其他 Subject 的区别

* **`RACSubject`**：不会缓存事件，新的订阅者无法收到之前发送的事件，只能接收订阅后发送的事件。
* **`RACReplaySubject`**：可以缓存所有事件或指定数量的历史事件，新订阅者会接收到所有缓存的事件。
* **`RACBehaviorSubject`**：只缓存最新的事件，新订阅者会接收到最后一个事件或初始值。

#### 适用场景

* **状态管理**：`RACBehaviorSubject` 非常适合用于需要保留当前状态的场景，如 UI 控件状态、加载状态等。
* **单一事件缓存**：当只需要缓存并重放最新的事件时，`RACBehaviorSubject` 是更轻量的选择。
* **默认初始值**：需要指定一个默认值，并保证在没有发送其他事件时，订阅者可以收到初始状态。

#### 总结

`RACBehaviorSubject` 是一种高效的信号类型，提供了最新事件的缓存和重放功能，适用于需要状态保持的场景。它的行为类似于只保留最新事件的 `RACReplaySubject`，但具有更简单的实现，适合用作信号的当前状态持有者。
