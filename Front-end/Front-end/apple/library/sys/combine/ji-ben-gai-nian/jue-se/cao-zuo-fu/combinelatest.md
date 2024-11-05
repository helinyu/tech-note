# combineLatest

`combineLatest` 是 `Combine` 中的一个操作符，它用于将多个 `Publisher` 的最新值合并在一起。当任意一个 `Publisher` 发出新值时，它会将所有其他 `Publisher` 当前的最新值与之一起组合，并将组合后的结果传递给下游。与 `zip` 不同的是，`combineLatest` 会在任意一个 `Publisher` 发出新值时更新组合后的输出，而不是等待每个 `Publisher` 都发出一个值。

#### `combineLatest` 操作符的基本用法

`combineLatest` 通过将多个 `Publisher` 的最新值组合在一起，生成一个新的 `Publisher`，每次其中任意一个 `Publisher` 发出新值时，都会触发新的组合事件。

**签名**

```swift
func combineLatest<P: Publisher>(_ other: P) -> Publishers.CombineLatest<Self, P>
```

你可以将多个 `Publisher` 使用 `combineLatest` 合并。

#### 示例：两个 `Publisher` 的 `combineLatest`

```swift
import Combine

let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<String, Never>()

let combinedSubscription = publisher1
    .combineLatest(publisher2)  // 合并两个 Publisher 的最新值
    .sink { (intValue, stringValue) in
        print("Int: \(intValue), String: \(stringValue)")
    }

publisher1.send(1)
publisher2.send("A")
publisher1.send(2)
publisher2.send("B")
```

#### 输出结果：

```
Int: 1, String: A
Int: 2, String: A
Int: 2, String: B
```

在这个示例中：

* `publisher1` 和 `publisher2` 分别发出整数和字符串。
* 每当其中一个 `Publisher` 发出新值时，`combineLatest` 会将两个 `Publisher` 当前的最新值组合并发出。

#### 示例：多个 `Publisher` 使用 `combineLatest`

你也可以将多个 `Publisher` 合并。`combineLatest` 会始终使用所有 `Publisher` 的最新值，每次任何一个 `Publisher` 发出新值时，都会触发组合事件。

```swift
import Combine

let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<String, Never>()
let publisher3 = PassthroughSubject<Double, Never>()

let combinedSubscription = publisher1
    .combineLatest(publisher2, publisher3)  // 合并三个 Publisher 的最新值
    .sink { (intValue, stringValue, doubleValue) in
        print("Int: \(intValue), String: \(stringValue), Double: \(doubleValue)")
    }

publisher1.send(1)
publisher2.send("A")
publisher3.send(10.0)

publisher1.send(2)
publisher2.send("B")

publisher3.send(20.0)
```

#### 输出结果：

```
Int: 1, String: A, Double: 10.0
Int: 2, String: A, Double: 10.0
Int: 2, String: B, Double: 10.0
Int: 2, String: B, Double: 20.0
```

在这个示例中：

* 每当任何一个 `Publisher` 发出新值时，`combineLatest` 都会将所有 `Publisher` 的最新值组合并传递给下游。
* 输出的顺序与哪个 `Publisher` 先发出值无关，而是依赖于哪个 `Publisher` 最近更新了值。

#### 工作原理

* **初始状态**：`combineLatest` 不会立即发出值，直到所有参与的 `Publisher` 都至少发出过一个值为止。只有在每个 `Publisher` 都有最新值时，才会开始发出组合结果。
* **更新输出**：每次任意一个 `Publisher` 发出新值时，`combineLatest` 都会将所有 `Publisher` 的最新值组合在一起，发给下游订阅者。
* **数据源变化**：`combineLatest` 确保你总是拿到每个 `Publisher` 的最新数据，而不是旧数据。
* **完成**：如果任意一个 `Publisher` 完成，`combineLatest` 也会停止发出值并通知下游完成。如果发生错误，`combineLatest` 会传递错误。

#### 示例：完成和错误处理

```swift
import Combine

let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<String, Never>()

let combinedSubscription = publisher1
    .combineLatest(publisher2)
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("All publishers finished.")
            case .failure(let error):
                print("Error: \(error)")
            }
        },
        receiveValue: { (intValue, stringValue) in
            print("Int: \(intValue), String: \(stringValue)")
        }
    )

publisher1.send(1)
publisher2.send("A")
publisher1.send(2)
publisher2.send("B")
publisher1.send(completion: .finished)
```

#### 输出结果：

```
Int: 1, String: A
Int: 2, String: A
Int: 2, String: B
All publishers finished.
```

在这个示例中：

* `publisher1` 完成后，`combineLatest` 也停止了发值。
* 只有当两个 `Publisher` 都发出至少一个值后，`combineLatest` 才会开始工作。

#### 与 `zip` 的区别

* `combineLatest` 会在任意一个 `Publisher` 发出新值时发出新的组合结果，且组合结果包含所有 `Publisher` 的最新值。
* `zip` 则是按顺序将每个 `Publisher` 发出的值配对，只有当每个 `Publisher` 都发出一个新值时才会触发事件。如果某个 `Publisher` 早于其他 `Publisher` 完成，`zip` 会停止发值。

#### 总结

* `combineLatest` 用于合并多个 `Publisher` 的最新值，并将它们按顺序组合成一个元组。
* 它会在任何一个 `Publisher` 发出新值时触发组合输出，每次都会使用所有 `Publisher` 的最新值。
* 适用于需要将多个流的最新数据实时组合并处理的场景。
* `combineLatest` 只会在所有的 `Publisher` 都发出过至少一个值后开始工作，确保每次输出都包含最新的数据。

`combineLatest` 非常适合需要同时关注多个数据源或事件流的场景，尤其是那些依赖于每个数据流的最新值来计算的场合。
