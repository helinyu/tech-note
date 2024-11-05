# switchToLatest

`switchToLatest` 是 `Combine` 中的一个操作符，用于处理嵌套的 `Publisher`。它会从一个发出 `Publisher` 的 `Publisher` 中“切换”到其中最新的那个 `Publisher`，并只关注当前活跃的 `Publisher` 的输出。这意味着它会丢弃其他先前的 `Publisher` 输出，始终只发出当前 `Publisher` 最新值。

#### `switchToLatest` 的工作原理

`switchToLatest` 主要用于处理那些发出 `Publisher` 的 `Publisher`（即“嵌套的 `Publisher`”）。当外层 `Publisher` 发出一个新的内部 `Publisher` 时，`switchToLatest` 会切换到新的内部 `Publisher`，并开始订阅该 `Publisher`。如果在此期间外层 `Publisher` 发出新的内部 `Publisher`，它会停止订阅当前的 `Publisher`，并切换到新的 `Publisher`。

#### 典型使用场景

1. **动态切换数据源**：当你有多个 `Publisher`，并且想要根据某些条件动态切换到当前活跃的 `Publisher` 时，`switchToLatest` 是一个非常合适的工具。例如，处理一个发出请求的 `Publisher`，当发出一个新的请求时，需要取消当前的请求并切换到新的请求。
2. **处理动态的流**：当你需要从多个流中选择一个活跃的流进行订阅，并且要丢弃不再活跃的流时，`switchToLatest` 可以帮助你简化逻辑。

#### 签名

```swift
func switchToLatest<Upstream: Publisher, Output>(_ upstream: Publishers.Map<Upstream, Publishers.SwitchToLatest<Output>>) -> Publishers.SwitchToLatest<Upstream>
```

`switchToLatest` 通常与其他操作符如 `map` 配合使用，用于发出一个新的 `Publisher`。

#### 示例：使用 `switchToLatest`

假设你有一个 `Publisher`，它发出的是其他 `Publisher`。你希望根据某些条件切换当前活跃的 `Publisher`，并只接收最新活跃 `Publisher` 的输出。

```swift
import Combine

// 定义一个发出 Publisher 的 Publisher
let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<Int, Never>()
let publisher3 = PassthroughSubject<Int, Never>()

let outerPublisher = PassthroughSubject<PassthroughSubject<Int, Never>, Never>()

let subscription = outerPublisher
    .switchToLatest() // 切换到内层 Publisher
    .sink { value in
        print("Received value: \(value)")
    }

outerPublisher.send(publisher1) // 订阅 publisher1
publisher1.send(1)
publisher1.send(2)

outerPublisher.send(publisher2) // 切换到 publisher2
publisher1.send(3)  // 这不会被接收
publisher2.send(4)
publisher2.send(5)

outerPublisher.send(publisher3) // 切换到 publisher3
publisher2.send(6)  // 这不会被接收
publisher3.send(7)
```

#### 输出结果：

```
Received value: 1
Received value: 2
Received value: 4
Received value: 5
Received value: 7
```

在这个示例中：

* `outerPublisher` 是一个 `Publisher`，它发出的是其他 `Publisher`（即 `publisher1`、`publisher2` 和 `publisher3`）。
* 当 `outerPublisher` 发出一个新的 `Publisher` 时，`switchToLatest` 会切换到新的内部 `Publisher`，并开始订阅它的输出。
* 每当内部的 `Publisher` 发出新的值时，`switchToLatest` 会更新输出，并丢弃之前的 `Publisher` 的值。

#### 工作原理总结

1. **外层 Publisher**：`switchToLatest` 需要一个外层 `Publisher`，它发出的是其他 `Publisher`。
2. **切换内部 Publisher**：每当外层 `Publisher` 发出一个新的内部 `Publisher` 时，`switchToLatest` 会停止对当前内部 `Publisher` 的订阅，并开始订阅新的 `Publisher`。
3. **丢弃旧的输出**：切换时，之前的 `Publisher` 输出会被丢弃，只有当前活跃的 `Publisher` 的输出会被传递给下游订阅者。
4. **处理动态数据流**：适用于你需要动态选择当前活跃的数据源，丢弃不再活跃的数据流的场景。

#### 示例：实际应用中的动态请求

假设你有多个网络请求，每个请求都是一个 `Publisher`，并且你只想保留最新发出的请求结果。例如，当用户快速点击按钮时，只有最后一次请求的结果是有效的。

```swift
import Combine

// 模拟网络请求的 Publisher
func networkRequest(id: Int) -> AnyPublisher<String, Never> {
    Just("Response from request \(id)")
        .delay(for: .seconds(1), scheduler: DispatchQueue.main) // 模拟延迟
        .eraseToAnyPublisher()
}

// 用于触发请求的 Publisher
let trigger = PassthroughSubject<Int, Never>()

// 外层 Publisher 发出请求 ID，内部是对应的网络请求
let subscription = trigger
    .map { networkRequest(id: $0) }  // 每次发出请求时映射到网络请求的 Publisher
    .switchToLatest()  // 只处理最新的请求结果
    .sink { response in
        print(response)
    }

trigger.send(1) // 发送第一个请求
trigger.send(2) // 发送第二个请求
trigger.send(3) // 发送第三个请求
```

#### 输出结果：

```
Response from request 3
```

在这个示例中：

* `trigger` 是一个触发网络请求的 `Publisher`，它发出请求的 ID。
* `networkRequest(id:)` 函数返回一个新的网络请求 `Publisher`，并模拟延迟。
* `switchToLatest` 会确保只有最后一个请求的响应结果被输出，之前的请求结果被丢弃。

#### 总结

* `switchToLatest` 适用于你需要切换处理不同的 `Publisher`，并只关注当前活跃 `Publisher` 的场景。
* 它会从多个发出 `Publisher` 的 `Publisher` 中选择最新的 `Publisher` 进行订阅，并丢弃之前的 `Publisher` 输出。
* 常用于动态的流控制，特别是在涉及多个选择或请求时，只关心最新的事件或数据源。

`switchToLatest` 是处理“动态流”场景的一个强大工具，能够简化多重数据流切换的逻辑。
