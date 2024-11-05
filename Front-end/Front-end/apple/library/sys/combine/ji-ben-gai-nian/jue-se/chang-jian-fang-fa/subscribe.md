# subscribe

#### 1. `subscribe` 方法

`subscribe` 方法用于启动一个订阅。它将一个订阅者（`Subscriber`）连接到发布者，使发布者开始发送数据事件到该订阅者。你通常不会直接调用 `subscribe` 方法，而是通过 `sink` 或 `assign` 等简便方法来创建并启动订阅。

**示例**：

```swift
swift复制代码let publisher = [1, 2, 3, 4, 5].publisher
let subscriber = Subscribers.Sink<Int, Never>(
    receiveCompletion: { completion in
        print("Completion: \(completion)")
    },
    receiveValue: { value in
        print("Received value: \(value)")
    }
)
publisher.subscribe(subscriber)
```

在这里：

* 我们使用了一个 `Subscribers.Sink` 实例作为订阅者，来处理发布者发出的数据。
* 调用 `subscribe` 将订阅者连接到发布者上，启动数据流。

**通常情况**： 在日常使用中，`subscribe` 方法很少被直接调用，因为 Combine 提供了更简便的方法，如 `sink` 和 `assign`，它们内部封装了 `subscribe`。



* `subscribe` 用于启动订阅，将发布者和订阅者连接起来。

