# Sink

在 `Combine` 框架中，`sink` 是一种常用的订阅方式，用于接收发布者（`Publisher`）发出的值或者完成事件。`sink` 可以用于处理 `Publisher` 发出的元素、处理完成事件，或者捕获错误。

`Sink` 是 `Subscriber` 协议的一部分，它不仅能接收 `Publisher` 发送的值，还可以处理 `Publisher` 完成或失败的状态。

#### 基本用法

`sink` 需要传入两个闭包，一个用于接收发出的值，另一个用于处理完成事件（包括成功或错误）。

**示例 1：接收值并处理完成事件**

```swift
import Combine

// 创建一个简单的Publisher
let publisher = [1, 2, 3, 4, 5].publisher

// 使用sink订阅Publisher
let subscription = publisher.sink { completion in
    switch completion {
    case .finished:
        print("Publisher completed successfully.")
    case .failure(let error):
        print("Publisher failed with error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}
```

**输出:**

```
Received value: 1
Received value: 2
Received value: 3
Received value: 4
Received value: 5
Publisher completed successfully.
```

在这个例子中，`sink` 用来订阅 `publisher` 并打印每个收到的值。当 `publisher` 完成时，`sink` 会调用 `finished` 处理闭包。

**示例 2：处理错误**

`Combine` 允许你通过 `sink` 捕获和处理错误。`Publisher` 可以发出 `.failure` 类型的事件，`sink` 会调用相应的错误处理闭包。

```swift
import Combine

enum MyError: Error {
    case someError
}

let publisher = Future<Int, MyError> { promise in
    // 模拟失败
    promise(.failure(.someError))
}

let subscription = publisher.sink { completion in
    switch completion {
    case .finished:
        print("Publisher completed successfully.")
    case .failure(let error):
        print("Publisher failed with error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}
```

**输出:**

```
Publisher failed with error: someError
```

**示例 3：简单的 `Just` Publisher**

`Just` 是一个非常基础的 `Publisher`，它只会发出一个值并且完成。通过 `sink` 订阅它，接收该值和完成事件。

```swift
import Combine

let publisher = Just(42)

let subscription = publisher.sink { completion in
    switch completion {
    case .finished:
        print("Completed")
    case .failure(let error):
        print("Failed with error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}
```

**输出:**

```
Received value: 42
Completed
```

#### 处理 `sink` 订阅的取消

当你使用 `sink` 创建一个订阅时，它会返回一个 `Cancellable` 对象。通过这个对象，你可以取消订阅。

```swift
import Combine

let publisher = [1, 2, 3].publisher

let subscription = publisher.sink { value in
    print("Received: \(value)")
}

// 取消订阅
subscription.cancel()
```

取消订阅后，`sink` 不会再接收来自 `publisher` 的值或事件。

#### `sink` 的参数说明

`sink` 方法有两种形式：

1. **接收值和完成事件：**

```swift
func sink(receiveCompletion: @escaping (Subscribers.Completion<Failure>) -> Void, 
          receiveValue: @escaping (Output) -> Void) -> AnyCancellable
```

* `receiveCompletion`: 接收 `Publisher` 完成状态，可能是 `.finished` 或 `.failure(error)`
* `receiveValue`: 用于处理 `Publisher` 发出的每个值

2. **仅接收值：**

```swift
func sink(receiveValue: @escaping (Output) -> Void) -> AnyCancellable
```

* 这种形式只会处理接收到的值，忽略完成事件和错误。

#### 使用场景

* **简单订阅**: `sink` 适用于快速的、简单的订阅需求，特别是当你需要处理异步任务的结果时。
* **UI更新**: 常用于将数据从 `Publisher`（如网络请求、数据库查询等）传递到 UI 层，自动更新界面。
* **错误处理**: `sink` 提供了一个方便的方式来捕获和处理流中的错误。

#### 总结

* `sink` 是 `Combine` 中非常重要的一个订阅工具，它可以接收 `Publisher` 发出的值，并处理完成和错误事件。
* `sink` 返回一个 `Cancellable` 对象，允许你在适当的时候取消订阅。
* `sink` 可以有两种形式：一种是同时处理接收到的值和完成事件，另一种只接收值。
