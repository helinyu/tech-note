# 对比

`PassthroughSubject` 和 `CurrentValueSubject` 都是 `Combine` 框架中的 `Publisher` 类型，它们的主要区别在于如何处理和保存数据。以下是两者的对比，帮助理解它们各自的特性和适用场景。

#### 1. **保存当前值**

* **`PassthroughSubject`**:
  * 不保存当前值。
  * 当新的订阅者订阅时，它只能接收到之后发布的事件，而不会收到先前的值。
  * 适合用于事件广播、信号或简单的通知系统，不能用作状态存储。
* **`CurrentValueSubject`**:
  * 保存当前值，新的订阅者会立即接收到这个当前值。
  * 每次发布新的值时，`CurrentValueSubject` 更新并广播该值。
  * 适合用于管理和传播当前状态（比如计数器、UI更新等），它可以作为数据绑定的一部分。

#### 2. **适用场景**

* **`PassthroughSubject`**:
  * 用于处理事件流，如按钮点击、网络请求完成、通知等。
  * 不关注历史状态，只关心事件的传播。
  * 典型使用场景：广播事件（如用户点击按钮）、异步回调的通知、信号传递。
* **`CurrentValueSubject`**:
  * 用于状态管理和数据流，其中需要维护并传播当前值。
  * 适合在应用中存储和广播当前状态，例如用户的输入值、UI 控件的状态、计数器等。
  * 典型使用场景：模型状态管理（如视图模型、计数器）、UI绑定（如 `UILabel` 绑定到视图模型的当前值）。

#### 3. **初始化**

*   **`PassthroughSubject`**:

    * 无需初始值，只是一个事件流的传递者。
    * 初始化时没有值，创建时不需要提供任何数据。

    ```swift
    let subject = PassthroughSubject<Int, Never>()
    ```
*   **`CurrentValueSubject`**:

    * 需要提供一个初始值。
    * 初始化时提供一个值，这个值会被保存，新的订阅者会首先接收到这个值。

    ```swift
    let subject = CurrentValueSubject<Int, Never>(0) // 初始值为 0
    ```

#### 4. **订阅者行为**

*   **`PassthroughSubject`**:

    * 新的订阅者只能接收到之后发布的事件。
    * 订阅者一开始不会收到任何历史值，只有从订阅开始之后发布的值。

    ```swift
    let subject = PassthroughSubject<Int, Never>()
    subject.send(1)  // 发布事件
    let subscription = subject.sink { value in
        print("Received: \(value)")
    }
    // 没有输出: "Received: 1"
    ```
*   **`CurrentValueSubject`**:

    * 新的订阅者会立即接收到当前的值。
    * 如果当前值是 `5`，即使订阅者在 `5` 之后才订阅，它仍然会接收到 `5`，然后接收随后的值。

    ```swift
    let subject = CurrentValueSubject<Int, Never>(0)
    subject.send(1)  // 当前值是 1
    let subscription = subject.sink { value in
        print("Received: \(value)")
    }
    // 输出: "Received: 1"
    ```

#### 5. **数据流**

* **`PassthroughSubject`**:
  * 仅仅传递新的值，并不会保存值。
  * 适用于事件流，不需要考虑状态保持和更新。
*   **`CurrentValueSubject`**:

    * 保存当前的值，可以随时通过 `.value` 属性访问当前值。
    * 每次更新时，都会广播新的值，并且新的订阅者可以立刻接收到当前值。

    ```swift
    let subject = CurrentValueSubject<Int, Never>(0)
    print(subject.value)  // 访问当前值，输出: 0
    subject.send(1)       // 更新为 1
    print(subject.value)  // 访问当前值，输出: 1
    ```

#### 6. **发布完成事件**

*   **`PassthroughSubject`**:

    * 可以发送 `.finished` 或 `.failure` 完成事件，通知订阅者事件流已经结束。

    ```swift
    subject.send(completion: .finished)
    ```
*   **`CurrentValueSubject`**:

    * 也可以发送 `.finished` 或 `.failure` 完成事件，但它会保留当前值，即使发送完成事件后，订阅者仍然可以访问 `.value`。

    ```swift
    subject.send(completion: .finished)
    print(subject.value)  // 完成后仍然可以访问值
    ```

#### 7. **内存管理**

* **`PassthroughSubject`**:
  * 它的生命周期与订阅者的生命周期相同。只要有订阅者，它会一直存在。如果没有订阅者，它会被释放。
* **`CurrentValueSubject`**:
  * 它的生命周期也与订阅者的生命周期相同，但是因为它会保持当前值，所以它是一个适合长时间存在的状态容器。

#### 8. **适合的错误类型**

* **`PassthroughSubject`**:
  * 它可以指定一个错误类型，但通常它用于不需要错误处理的简单事件流。如果你使用它时不需要错误传播，可以使用 `Never` 作为错误类型。
* **`CurrentValueSubject`**:
  * 也可以指定错误类型，并且如果你需要持有并传播状态的同时处理错误，`CurrentValueSubject` 是一个非常合适的选择。

#### 对比总结表

| 特性          | `PassthroughSubject` | `CurrentValueSubject` |
| ----------- | -------------------- | --------------------- |
| **是否保存当前值** | 不保存当前值               | 保留并广播当前值              |
| **订阅者行为**   | 新订阅者接收到之后发布的事件       | 新订阅者接收到当前值和之后的事件      |
| **初始化时需要值** | 无需初始值                | 需要一个初始值               |
| **适用场景**    | 用于事件流、信号通知等          | 用于状态管理、当前值绑定等         |
| **能否访问当前值** | 不可访问当前值              | 可以通过 `.value` 属性访问当前值 |
| **适合错误类型**  | 支持错误类型               | 支持错误类型                |
| **生命周期**    | 随着订阅者的生命周期而存在        | 可以长期存在并保存当前值          |
| **典型使用场景**  | 用户点击、事件通知、异步回调       | UI状态绑定、模型数据状态管理、计数器等  |

#### 总结

* **`PassthroughSubject`** 更适合用于**事件驱动**的场景，它只广播新事件，不关注保存任何值，适用于需要广播信号或通知的情况。
* **`CurrentValueSubject`** 更适合用于需要管理**当前状态**的场景，它保存并广播当前值，适用于应用程序状态的共享和动态更新，尤其是当你希望新的订阅者能够访问到当前状态时。
