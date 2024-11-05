# merge

在 `Combine` 中，<mark style="color:red;">`merge`</mark> <mark style="color:red;"></mark><mark style="color:red;">操作符用于将多个</mark> <mark style="color:red;"></mark><mark style="color:red;">`Publisher`</mark> <mark style="color:red;"></mark><mark style="color:red;">的输出合并成一个流</mark>。所有合并后的 `Publisher` 会并发地发出值，并将它们按接收到的顺序传递给下游订阅者，直到所有的 `Publisher` 完成。

#### `merge` 操作符的基本用法

`merge` 操作符接受一个或多个 `Publisher`，并将它们的值合并成一个流。每个 `Publisher` 会按顺序发出它们的值，直到它们的输出流完成。

**签名**

```swift
func merge<P: Publisher>(_ other: P) -> Publishers.Merge<Self, P>
```

如果有多个 `Publisher`，你可以使用 `merge` 将它们合并。

#### 示例：合并两个 `Publisher`

```swift
import Combine

let publisher1 = [1, 2, 3].publisher
let publisher2 = [4, 5, 6].publisher

let mergedSubscription = publisher1
    .merge(with: publisher2)  // 合并两个 Publisher
    .sink { value in
        print(value)  // 输出: 1, 4, 2, 5, 3, 6（输出顺序根据接收到的顺序）
    }
```

在这个示例中：

* `publisher1` 和 `publisher2` 是两个发出整数的 `Publisher`。
* 使用 `merge(with:)` 将两个 `Publisher` 合并为一个流。
* 最终，`sink` 会接收两个 `Publisher` 按照它们发出的顺序发出的所有值。

#### 处理多个 `Publisher`

`merge` 操作符支持多个 `Publisher`，你可以通过将多个 `Publisher` 放在一个数组或集合中进行合并。以下是将多个 `Publisher` 合并的示例：

```swift
import Combine

let publisher1 = [1, 2].publisher
let publisher2 = [3, 4].publisher
let publisher3 = [5, 6].publisher

let mergedSubscription = Publishers.MergeMany(publisher1, publisher2, publisher3)
    .sink { value in
        print(value)  // 输出: 1, 3, 2, 4, 5, 6（输出顺序根据接收到的顺序）
    }
```

在此示例中：

* `Publishers.MergeMany` 合并了多个 `Publisher`（`publisher1`, `publisher2`, `publisher3`）。
* 合并后的流会按各个 `Publisher` 接收到的顺序依次发出值。

#### 工作原理

* 每个 `Publisher` 会并发发出它的值，这意味着它们的值并不会按顺序等待对方的输出。
* 如果一个 `Publisher` 比其他的先完成，合并后的流依然会继续接收其他 `Publisher` 的值，直到所有 `Publisher` 都完成。
* `merge` 不会对事件进行排序，它只会把每个 `Publisher` 发出的值按接收到的顺序传递给下游。

#### 示例：`merge` 和 `Completion`

`merge` 操作符会在所有合并的 `Publisher` 完成时发送一个 `.finished` 事件。直到所有的 `Publisher` 完成，它才会发送完成事件。如果其中一个 `Publisher` 出现错误，则合并流会立即结束并发出错误。

```swift
import Combine

let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<Int, Never>()

let mergedSubscription = publisher1
    .merge(with: publisher2)  // 合并两个 Publisher
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("All Publishers finished.")
            case .failure(let error):
                print("Error: \(error)")
            }
        },
        receiveValue: { value in
            print(value)  // 输出: 1, 2, 3, 4
        }
    )

publisher1.send(1)
publisher2.send(2)
publisher1.send(3)
publisher2.send(4)
publisher1.send(completion: .finished)  // 输出: All Publishers finished.
publisher2.send(completion: .finished)
```

在这个示例中：

* `publisher1` 和 `publisher2` 使用 `PassthroughSubject` 创建。
* `merge` 会将两个 `Publisher` 合并成一个流，并且发出的所有值都将传递给下游。
* 当所有的 `Publisher` 完成时，`sink` 会接收到一个 `.finished` 完成事件。

#### 使用场景

`merge` 操作符非常适合以下场景：

1. **多个并发数据源**：当你有多个并发的数据源（比如多个网络请求、事件流等），`merge` 可以将这些数据源的输出合并为一个流，统一处理。
2. **同时监听多个事件**：如果你想同时监听多个事件（例如多个按钮点击、多个状态更新等），`merge` 可以将这些事件合并并集中处理。
3. **异步任务合并**：在处理异步任务时，`merge` 允许你将多个异步操作的结果合并成一个流，避免逐一处理每个异步任务的输出。

#### 总结

* `merge` 操作符允许你将多个 `Publisher` 合并成一个流，所有 `Publisher` 会并发地发出值，并按接收到的顺序传递给下游。
* 如果有多个 `Publisher`，你可以使用 `Publishers.MergeMany` 来合并它们。
* `merge` 操作符适用于多个并发数据源或事件流的场景，让你能够统一处理来自多个源的数据。
