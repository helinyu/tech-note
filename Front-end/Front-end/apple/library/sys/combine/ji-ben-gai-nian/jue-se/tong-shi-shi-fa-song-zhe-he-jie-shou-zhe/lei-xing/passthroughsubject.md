# PassthroughSubject

在 `Combine` 框架中，`PassthroughSubject` 是一个非常有用的类型，它可以作为一个 `Publisher` 来发出事件。与 `CurrentValueSubject` 不同，`PassthroughSubject` 只会发出新的事件，并不会保持任何值的状态。它是一个"简单的"发布者，通常用来将数据从一个部分传播到另一个部分，并允许对外部订阅者进行广播。

`PassthroughSubject` 在处理和传播事件（比如按钮点击、网络响应等）时非常有用。它可以在运行时动态地发布新的值、事件或错误。

#### 创建和使用 `PassthroughSubject`

`PassthroughSubject` 是一个泛型类型，它接受两个类型参数：

* **Output**: 发布的数据类型。
* **Failure**: 错误类型，必须符合 `Error` 协议。

#### 基本用法

```swift
import Combine

// 创建一个PassthroughSubject，它发出的值是Int类型，错误类型是Error
let passthroughSubject = PassthroughSubject<Int, Error>()

// 创建一个订阅者
let subscription = passthroughSubject.sink { completion in
    switch completion {
    case .finished:
        print("Finished")
    case .failure(let error):
        print("Error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}

// 发布值
passthroughSubject.send(1)
passthroughSubject.send(2)
passthroughSubject.send(3)

// 完成Publisher
passthroughSubject.send(completion: .finished)
```

**输出:**

```
Received value: 1
Received value: 2
Received value: 3
Finished
```

在这个示例中，`passthroughSubject` 发布了三个值，并在最后发送了 `.finished` 完成事件。订阅者接收到这些值并打印出来。

#### 发送值

`PassthroughSubject` 提供了几个关键方法来发送值或事件：

1.  **send(\_:)**: 发布一个值，所有订阅者都会接收到这个值。

    ```swift
    passthroughSubject.send(42)
    ```
2.  **send(completion:)**: 发送一个完成事件，告诉订阅者这个流已经结束。可以是 `.finished` 或 `.failure(error)`。

    ```swift
    passthroughSubject.send(completion: .finished) // 完成事件
    passthroughSubject.send(completion: .failure(MyError.someError)) // 错误事件
    ```

#### 订阅和接收值

`PassthroughSubject` 遵循 `Publisher` 协议，因此可以使用 `.sink` 或其他的 `Subscriber` 订阅它，接收它发出的值。

```swift
let subscription = passthroughSubject.sink { value in
    print("Received value: \(value)")
}
```

#### 处理错误

`PassthroughSubject` 也能发出错误事件（`failure`），你可以在订阅时捕获这个错误并进行处理。

```swift
enum MyError: Error {
    case someError
}

let passthroughSubject = PassthroughSubject<Int, MyError>()

let subscription = passthroughSubject.sink { completion in
    switch completion {
    case .finished:
        print("Finished")
    case .failure(let error):
        print("Error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}

// 发布值
passthroughSubject.send(1)
passthroughSubject.send(2)

// 发送错误事件
passthroughSubject.send(completion: .failure(.someError))
```

**输出:**

```
Received value: 1
Received value: 2
Error: someError
```

#### 与其他Publisher结合使用

你可以将 `PassthroughSubject` 与其他类型的 `Publisher` 结合使用，比如通过 `map`、`flatMap` 等操作符处理发布的数据。

```swift
let passthroughSubject = PassthroughSubject<Int, Never>()

let subscription = passthroughSubject
    .map { $0 * 2 }  // 每个值乘以2
    .sink { value in
        print("Received mapped value: \(value)")
    }

passthroughSubject.send(1)
passthroughSubject.send(2)
passthroughSubject.send(3)
```

**输出:**

```
Received mapped value: 2
Received mapped value: 4
Received mapped value: 6
```

#### 取消订阅

`PassthroughSubject` 返回的 `Cancellable` 对象可以用来取消订阅。当你不再需要接收事件时，可以调用 `cancel()` 来停止接收。

```swift
let subscription = passthroughSubject.sink { value in
    print("Received value: \(value)")
}

// 取消订阅
subscription.cancel()
```

#### 典型使用场景

* **事件广播**: `PassthroughSubject` 非常适合事件的广播，如按钮点击、用户操作等。
* **状态更新**: 用于在多个部分之间传递事件，比如网络请求完成时通知其他组件。
* **动态数据流**: 在需要动态发送数据的场景中，`PassthroughSubject` 是一个很好的选择。

#### `PassthroughSubject` 与 `CurrentValueSubject` 的区别

* **PassthroughSubject**:
  * 不会保留历史值。
  * 仅发送新的事件给订阅者。
  * 适用于广播事件或动态值传递。
* **CurrentValueSubject**:
  * 会保留最近发送的值。
  * 新的订阅者会收到当前的值。
  * 适用于需要在多个地方访问最近状态的情况。

#### 总结

* `PassthroughSubject` 是 `Combine` 中用于发出事件的一个非常基础和灵活的类型。
* 它适合用于事件驱动的场景，例如用<mark style="color:orange;">户输入、网络请求完成</mark>等。
* 它允许你手动控制发送的数据流和事件（例如，发送值或错误事件）。
* `PassthroughSubject` 是一个非常简洁的 `Publisher`，可以与其他 `Combine` 操作符结合，进行强大的流式处理。

通过使用 `PassthroughSubject`，你可以灵活地将异步操作、事件或状态更改传播到应用程序的其他部分。
