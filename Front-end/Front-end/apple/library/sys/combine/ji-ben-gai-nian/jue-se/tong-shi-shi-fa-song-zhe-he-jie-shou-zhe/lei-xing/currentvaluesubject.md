# CurrentValueSubject

`CurrentValueSubject` 是 `Combine` 框架中的一个 `Publisher`，它在某些情况下比 `PassthroughSubject` 更有用，<mark style="color:red;">尤其是在需要保存当前值并允许新的订阅者访问这个值时</mark>。与 `PassthroughSubject` 不同，`CurrentValueSubject` 不仅会广播新的事件，还会保留最近发送的值，因此新的订阅者能够立即获得这个值。

#### `CurrentValueSubject` 的特点

* **保留当前值**：`CurrentValueSubject` 总是持有它的最新值，并且新的订阅者会立即接收到这个最新的值。
* **发送新的值**：和 `PassthroughSubject` 一样，`CurrentValueSubject` 也会发出新的值。
* **初始化时需要一个初始值**：`CurrentValueSubject` 需要一个初始值来开始它的生命周期。
* **适用于状态管理**：由于它能够持有并广播当前的值，`CurrentValueSubject` 非常适用于需要维护应用状态的场景。

#### 初始化 `CurrentValueSubject`

`CurrentValueSubject` 是一个泛型类型，需要提供两个类型参数：

1. **Output**: 发布的数据类型。
2. **Failure**: 错误类型，必须符合 `Error` 协议。

```swift
let subject = CurrentValueSubject<Int, Never>(0) // 初始值为 0，错误类型为 Never（即没有错误）
```

#### 基本用法

创建一个 `CurrentValueSubject`，你可以给它提供一个初始值，之后就可以像其他 `Publisher` 一样向其发送新的值。

```swift
import Combine

// 创建一个CurrentValueSubject，初始值为0，错误类型为Never（没有错误）
let subject = CurrentValueSubject<Int, Never>(0)

// 订阅该Publisher
let subscription = subject.sink { value in
    print("Received value: \(value)")
}

// 发布一些新的值
subject.send(1)
subject.send(2)
subject.send(3)

// 输出:
// Received value: 0   // 初始值
// Received value: 1
// Received value: 2
// Received value: 3
```

#### 新的订阅者会收到最新的值

`CurrentValueSubject` 会保存它的最新值，因此新的订阅者会收到这个最新的值，而不仅仅是接收之后的事件。

```swift
import Combine

let subject = CurrentValueSubject<Int, Never>(0)

let firstSubscriber = subject.sink { value in
    print("First subscriber received value: \(value)")
}

subject.send(1)
subject.send(2)

// 第二个订阅者会立即接收到最新的值
let secondSubscriber = subject.sink { value in
    print("Second subscriber received value: \(value)")
}

subject.send(3)

// 输出:
// First subscriber received value: 0
// First subscriber received value: 1
// First subscriber received value: 2
// Second subscriber received value: 2
// First subscriber received value: 3
// Second subscriber received value: 3
```

在这个例子中，第二个订阅者在订阅时接收到 `CurrentValueSubject` 的当前值（即 2），而不仅仅是从它订阅后开始发出的新值。

#### 发送值

和 `PassthroughSubject` 一样，`CurrentValueSubject` 也能通过 `send(_:)` 来发送新的值。新的值会被所有订阅者接收到，并且会更新 `CurrentValueSubject` 的当前值。

```swift
subject.send(4)  // 更新并广播新的值
```

#### 订阅并使用当前值

因为 `CurrentValueSubject` 会持有并广播当前的值，它非常适合用于状态管理和视图绑定等场景。每次状态变化时，`CurrentValueSubject` 会广播新的值，并允许新的订阅者直接访问最新的状态。

#### 示例：用作状态管理

假设我们有一个 `ViewModel`，我们希望它能够通知视图更新，并且每次视图需要显示最新的状态时，它都能从 `ViewModel` 获取当前的状态。

```swift
import Combine

class ViewModel {
    // 使用CurrentValueSubject管理状态
    var counter = CurrentValueSubject<Int, Never>(0)
    
    func incrementCounter() {
        // 增加计数器值
        counter.send(counter.value + 1)
    }
}

let viewModel = ViewModel()

// 订阅ViewModel的counter属性
let subscription = viewModel.counter.sink { value in
    print("Counter updated: \(value)")
}

// 增加计数器
viewModel.incrementCounter() // 输出: Counter updated: 1
viewModel.incrementCounter() // 输出: Counter updated: 2
```

在这个例子中，`CurrentValueSubject` 用来保持 `counter` 的当前值，并且每当值变化时，所有订阅者都会接收到新的值。

#### 结合其他操作符使用

`CurrentValueSubject` 作为一个 `Publisher`，可以与其他 `Combine` 操作符结合使用，比如 `map`、`filter` 等。你可以将它作为数据流的一部分，进行处理和转换。

```swift
let mappedSubscription = subject
    .map { $0 * 2 }
    .sink { value in
        print("Mapped value: \(value)")
    }

subject.send(4)  // 输出: Mapped value: 8
```

#### 处理错误

`CurrentValueSubject` 可以与 `Publisher` 结合使用，但它也可以指定错误类型。比如，你可以指定错误类型为 `Never`，表示它不会发出错误。

```swift
let subject = CurrentValueSubject<Int, Never>(0)

// 无错误类型
subject.send(5)
```

如果你想使用 `CurrentValueSubject` 处理错误事件，可以指定一个符合 `Error` 协议的错误类型。

```swift
enum MyError: Error {
    case somethingWentWrong
}

let subject = CurrentValueSubject<Int, MyError>(0)
subject.send(1)
subject.send(completion: .failure(MyError.somethingWentWrong))
```

#### 与 `PassthroughSubject` 的区别

* **`PassthroughSubject`**：不保存任何值，每次新的订阅者只会收到从它订阅后开始发布的事件。
* **`CurrentValueSubject`**：保存当前值，新的订阅者会立即收到当前值，并且它会在发布新的值时更新。

#### 总结

* `CurrentValueSubject` 是 `Combine` 中一个非常有用的类型，适用于需要保存当前状态并让新订阅者能够立即获取该状态的场景。
* 它适合用于状态管理和动态数据绑定等应用程序中。
* 新的订阅者会立即接收到当前值，而不仅仅是之后的事件。
* 与 `PassthroughSubject` 相比，`CurrentValueSubject` 更适合用于那些需要保留当前状态的场景。
