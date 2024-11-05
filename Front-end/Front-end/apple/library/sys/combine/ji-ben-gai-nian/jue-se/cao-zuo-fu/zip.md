# zip

在 `Combine` 中，`zip` 操作符用于将多个 `Publisher` 的输出按顺序配对。当每个 `Publisher` 发出新值时，`zip` 会等待其他 `Publisher` 也发出一个新值，然后将这些值组合成一个元组（tuple）并发给下游。如果某个 `Publisher` 早于其他 `Publisher` 完成或停止发值，`zip` 会停止发出新值。

#### `zip` 操作符的基本用法

`zip` 操作符会组合来自多个 `Publisher` 的值，直到其中一个 `Publisher` 完成或发生错误。它会按顺序将每个 `Publisher` 发出的值配对，每个配对是一个元组，包含所有 `Publisher` 当前的最新值。

**签名**

```swift
func zip<P: Publisher, Q: Publisher>(
    _ other: Q
) -> Publishers.Zip<Self, Q>
```

你可以将多个 `Publisher` 配对并将它们的输出合并成一个元组，直到任何一个 `Publisher` 完成。

#### 示例：基本的 `zip`

```swift
import Combine

let publisher1 = [1, 2, 3].publisher
let publisher2 = ["A", "B", "C"].publisher

let zippedSubscription = publisher1
    .zip(publisher2)  // 将两个 Publisher 配对
    .sink { (intValue, stringValue) in
        print("Int: \(intValue), String: \(stringValue)")
    }
```

#### 输出结果：

```
Int: 1, String: A
Int: 2, String: B
Int: 3, String: C
```

在这个示例中：

* `publisher1` 和 `publisher2` 是两个 `Publisher`，分别发出整数和字符串。
* `zip` 会将它们的输出按顺序组合成一个元组（`Int`, `String`），并将每对值传递给下游订阅者。

#### 示例：多个 `Publisher` 使用 `zip`

如果你有多个 `Publisher`，你可以使用 `zip` 来将它们配对并组合成一个元组。例如，合并三个 `Publisher` 的输出：

```swift
import Combine

let publisher1 = [1, 2, 3].publisher
let publisher2 = ["A", "B", "C"].publisher
let publisher3 = [10.0, 20.0, 30.0].publisher

let zippedSubscription = publisher1
    .zip(publisher2, publisher3)  // 将三个 Publisher 配对
    .sink { (intValue, stringValue, doubleValue) in
        print("Int: \(intValue), String: \(stringValue), Double: \(doubleValue)")
    }
```

#### 输出结果：

```
Int: 1, String: A, Double: 10.0
Int: 2, String: B, Double: 20.0
Int: 3, String: C, Double: 30.0
```

#### 工作原理

* `zip` 会等待每个 `Publisher` 发出一个值，然后将这些值组合成一个元组，并将这个元组传递给下游。
* 每当任意一个 `Publisher` 发出新值时，`zip` 会从所有 `Publisher` 中取出最新的值并配对。
* 一旦某个 `Publisher` 完成或出错，`zip` 就会停止发出新值。**如果某个 `Publisher` 的值不足以配对（例如，一个流比其他流快完成），`zip` 将不会发出任何剩余的值**。

#### 示例：不对称长度的 `Publisher`

如果一个 `Publisher` 比其他 `Publisher` 快完成（例如，某个 `Publisher` 的值较少），`zip` 会停止发出值，而不会继续等待其他流。

```swift
import Combine

let publisher1 = [1, 2].publisher
let publisher2 = ["A", "B", "C"].publisher

let zippedSubscription = publisher1
    .zip(publisher2)  // 将两个 Publisher 配对
    .sink { (intValue, stringValue) in
        print("Int: \(intValue), String: \(stringValue)")
    }
```

#### 输出结果：

```
Int: 1, String: A
Int: 2, String: B
```

在这个示例中：

* `publisher1` 只包含两个值，而 `publisher2` 包含三个值。
* 因为 `zip` 会等待所有 `Publisher` 提供值，所以一旦 `publisher1` 发完所有值，`zip` 会停止，`publisher2` 中剩余的值不会被发出。

#### 错误处理

如果在任何一个 `Publisher` 中发生错误，`zip` 会停止并将错误传递给下游。可以使用 `tryCatch` 或类似的操作符来处理错误。

```swift
import Combine

let publisher1 = [1, 2, 3].publisher
let publisher2 = [5, 6, 7].publisher

let errorPublisher = Fail<Int, Never>(error: NSError(domain: "Example", code: 0, userInfo: nil))

let zippedSubscription = publisher1
    .zip(publisher2)
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Completed")
            case .failure(let error):
                print("Error: \(error)")
            }
        },
        receiveValue: { (intVal, stringVal) in
            print("Int: \(intVal), String: \(stringVal)")
        }
    )

// 一旦发生错误，zip 会停止
errorPublisher.send(completion: .failure(NSError(domain: "Example", code: 0, userInfo: nil)))
```

#### 总结

* `zip` 是 `Combine` 中的一个操作符，用于按顺序将多个 `Publisher` 的值配对。
* 它会等到每个 `Publisher` 都发出一个值时才会发出组合后的元组。如果某个 `Publisher` 的值不足以配对，`zip` 会停止发值。
* `zip` 用于在多个流中同步处理数据，常用于需要按顺序处理来自不同数据源的相关信息的场景。
* 如果任何一个 `Publisher` 完成或发生错误，`zip` 将停止发出值并传递相应的事件。

`zip` 是一种强大的操作符，适合处理多个数据流的同步操作，尤其是当多个流之间的数据关系需要按照顺序进行<mark style="color:red;">匹配</mark>时。
