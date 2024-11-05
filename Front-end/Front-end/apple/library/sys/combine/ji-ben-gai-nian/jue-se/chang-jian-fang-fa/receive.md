# receive

在 Swift Combine 框架中，`receive` 方法是 `Subscriber` 协议的一部分，允许订阅者处理来自发布者（Publisher）的数据和完成事件。这个方法主要有两个变体，用于接收值和处理完成事件。

#### `receive` 方法的变体

**1. 接收值的方法**

```swift
func receive(_ input: Input) -> Subscribers.Demand
```

* **参数**:
  * `input`: 这是发布者发送的值，类型为 `Input`，即发布者的输出类型。
* **返回值**:
  * 返回一个 `Subscribers.Demand` 类型，表示订阅者希望接收更多的数据的数量或策略。

**用途**:

* 在这个方法中，订阅者可以处理接收到的值，通常会在这里执行某种操作（例如，打印、存储、更新UI等）。
* 你可以根据处理逻辑决定要请求多少更多的值，例如返回 `.max(n)` 请求更多值或返回 `.none` 表示不再请求。

**示例**:

```swift
struct IntSubscriber: Subscriber {
    typealias Input = Int
    typealias Failure = Never

    func receive(subscription: Subscription) {
        subscription.request(.max(3))  // 请求最多接收 3 个值
    }

    func receive(_ input: Int) -> Subscribers.Demand {
        print("Received value: \(input)")
        return .none  // 不请求额外的值
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Completed: \(completion)")
    }
}

let publisher = [1, 2, 3, 4, 5].publisher
let subscriber = IntSubscriber()
publisher.subscribe(subscriber)
```

**2. 接收完成的方法**

```swift
func receive(completion: Subscribers.Completion<Failure>)
```

* **参数**:
  * `completion`: 这是一个 `Subscribers.Completion` 类型的值，指示发布者是正常完成（`.finished`）还是由于错误而失败（`.failure`）。
* **用途**:
  * 这个方法用于处理数据流的结束情况。订阅者可以在此处进行清理或更新状态等操作。

**示例**:

```swift
func receive(completion: Subscribers.Completion<Never>) {
    switch completion {
    case .finished:
        print("The publisher has completed successfully.")
    case .failure(let error):
        print("The publisher failed with error: \(error)")
    }
}
```

#### 完整的 `Subscriber` 实现示例

下面是一个完整的示例，展示了如何实现一个自定义的 `Subscriber`，并使用 `receive` 方法处理来自发布者的事件：

```swift
import Combine

struct CustomSubscriber: Subscriber {
    typealias Input = Int
    typealias Failure = Never

    func receive(subscription: Subscription) {
        print("Subscribed")
        subscription.request(.unlimited) // 请求无限数量的数据
    }

    func receive(_ input: Int) -> Subscribers.Demand {
        print("Received value: \(input)")
        return .none // 不再请求更多值
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Completed with: \(completion)")
    }
}

let publisher = (1...5).publisher
let customSubscriber = CustomSubscriber()
publisher.subscribe(customSubscriber)
```

#### 关键点总结

* `receive(_:)` 方法用于处理从发布者接收到的每个值，并返回一个 `Subscribers.Demand`，指示接下来希望接收多少数据。
* `receive(completion:)` 方法用于处理发布者发送的完成事件，允许订阅者在数据流结束时执行适当的操作。

通过实现 `Subscriber` 协议，开发者可以创建自定义的订阅者来响应数据流和事件，灵活地控制数据的接收和处理逻辑。
