# 接受者

在 Combine 框架中，接收者（Subscriber）的类型有几种。主要的接收者类型包括：

1. **`Subscriber` 协议**\
   `Subscriber` 是 Combine 框架中所有接收者的基础协议。它定义了接收事件的接口，所有接收者都需要遵循这个协议。具体实现时，`Subscriber` 可以分为以下几种类型。
2. **`AnySubscriber`**\
   `AnySubscriber` 是一个通用的 Subscriber 类型，它封装了一个具体的 Subscriber，提供了类型擦除。你可以通过 `AnySubscriber` 来避免暴露具体的 Subscriber 类型，常用于需要将不同类型的 Subscriber 传递或存储的场景。
3.  **`Sink`**\
    `Sink` 是一种常用的 Subscriber，它有两个闭包：一个用于接收数据（`receiveValue`），一个用于接收完成事件（`receiveCompletion`）。你可以使用 `sink(receiveValue:)` 或 `sink(receiveCompletion:receiveValue:)` 来创建一个 `Sink`。

    示例：

    ```swift
    let publisher = Just(42)
    let subscriber = publisher.sink(receiveValue: { value in
        print(value)
    })
    ```
4.  **`Assign`**\
    `Assign` 是一种特化的 Subscriber，用于将接收到的值赋给某个对象的属性。它非常适合于将数据流直接绑定到 UI 元素上。通常用于绑定 `@Published` 属性或 UI 元素的值。

    示例：

    ```swift
    class MyModel {
        @Published var value: Int = 0
    }

    let model = MyModel()
    let publisher = Just(42)
    let subscriber = publisher.assign(to: \.value, on: model)
    ```
5.  **`PassthroughSubject` 和 `CurrentValueSubject`**\
    `PassthroughSubject` 和 `CurrentValueSubject` 都是既可以作为 Publisher 也可以作为 Subscriber 使用的类型。它们会接收值并将其发布出去。`PassthroughSubject` 没有初始值，而 `CurrentValueSubject` 在初始化时有一个初始值，并且会在订阅时立即发送该值。

    示例：

    ```swift
    let subject = PassthroughSubject<Int, Never>()
    let subscriber = subject.sink(receiveValue: { value in
        print(value)
    })
    subject.send(42)
    ```
6.  **`Cancellable`**\
    `Cancellable` 本身并不直接是一个 Subscriber，但它是一个类型，表示对订阅的引用。你可以使用 `Cancellable` 来取消订阅，通常是在收到一个 Subscriber 后，返回一个 `Cancellable` 类型的对象。

    示例：

    ```swift
    let cancellable = publisher.sink(receiveValue: { value in
        print(value)
    })
    cancellable.cancel()  // 取消订阅
    ```

总结来说，Combine 中的接收者类型主要包括基础的 `Subscriber` 协议，以及具体实现如 `Sink`、`Assign`、`PassthroughSubject` 和 `CurrentValueSubject` 等。它们根据不同的用途提供了不同的功能。
