# Just

`Just` 是 Combine 中的一个简单发布者，它会发布一个单一的值并立即完成。它是一个很基础的发布者，用于快速传递一个值到订阅者，通常用于测试或简单的场景中。

#### 使用示例：

1.  **基本用法**： `Just` 用来创建一个只发布单一值的发布者。

    ```swift
    import Combine

    let publisher = Just(42)  // 创建一个发布者，发布值 42
    let subscription = publisher
        .sink(receiveValue: { value in
            print("Received value: \(value)")
        })
    ```

    **输出：**

    ```
    Received value: 42
    ```

    这段代码中，`Just(42)` 创建了一个发布者，它发布值 `42` 并立即完成。`sink` 方法是订阅者，用于接收和处理发布的值。
2. **发布者的生命周期**： `Just` 发布者在发布完数据后会立刻完成，不会发出错误或进一步的事件。如果你订阅它，它会立即发出值并完成。
3.  **与 `sink` 一起使用**： `sink` 是一个订阅者，它接受一个闭包用于处理发布的值。它还可以处理完成事件和错误事件，尽管 `Just` 不会发布错误。

    ```swift
    let publisher = Just("Hello, Combine!")
    let subscription = publisher
        .sink(receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Publisher completed successfully.")
            case .failure(let error):
                print("Publisher failed with error: \(error)")
            }
        }, receiveValue: { value in
            print("Received value: \(value)")
        })
    ```

    **输出：**

    ```
    Received value: Hello, Combine!
    Publisher completed successfully.
    ```
4.  **类型注解**： `Just` 需要明确知道它发布的值的类型，如果传递的是一个没有类型注解的常量，Swift 编译器可能会要求你指定类型。

    ```swift
    let publisher: Just<Int> = Just(3)  // 明确声明为 Int 类型的 Just 发布者
    ```

#### 特点：

* 仅发布一个值并立即完成。
* 不会产生错误，`Just` 发布者的 `Failure` 类型是 `Never`。
* 简单易用，通常用于简单的场景或作为测试用的 mock 发布者。

#### 与其他发布者的比较：

`Just` 与 `PassthroughSubject` 的主要区别是：`Just` 只发布一个值并完成，而 `PassthroughSubject` 可以动态地发布多个值，并且没有完成或错误的强制要求。
