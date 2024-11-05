# share/muticast

在 Swift Combine 框架中，`share()` 和 `multicast` 都是用来共享发布者（Publisher）的输出流的，但它们有一些不同的应用场景和实现方式：

#### 1. `share()`

* `share()` 是一个共享发布者的简便方法，用于让多个订阅者订阅同一个数据流，并且每个订阅者都会接收到同样的数据。
* 它是使用 `multicast` 的一种简化版本，相当于调用 `multicast` 并传入 `PassthroughSubject()`，然后自动连接。
* 共享后的发布者会在有第一个订阅者时自动连接，并在所有订阅者取消订阅后断开连接。
* 适合用在数据源不需要手动控制时的情况。

**示例：**

```swift
let sharedPublisher = publisher.share()
sharedPublisher.sink { value in print("Subscriber 1: \(value)") }
sharedPublisher.sink { value in print("Subscriber 2: \(value)") }
```

#### 2. `multicast`

* `multicast` 是一种更加灵活的操作符，允许你提供一个 `Subject`，如 `PassthroughSubject` 或 `CurrentValueSubject`，来控制数据的发布。
* 使用 `multicast` 后，你需要手动调用 `.connect()` 来启动数据流。
* 适合于希望对发布行为有更精细控制的场景，如希望在特定时间点发送数据，或者在多个订阅者订阅前缓存一些数据。

**示例：**

```swift
let subject = PassthroughSubject<Int, Never>()
let multicastPublisher = publisher.multicast(subject: subject)

multicastPublisher.sink { value in print("Subscriber 1: \(value)") }
multicastPublisher.sink { value in print("Subscriber 2: \(value)") }

// 手动连接以启动数据流
let connection = multicastPublisher.connect()

// 断开连接（可选）
connection.cancel()
```

#### 选择哪个？

* 如果不需要手动控制连接和断开，且只是简单的共享数据流，`share()` 就足够。
* 如果需要在订阅之前准备数据，或希望对流的启动和停止进行控制，`multicast` 更适合。
