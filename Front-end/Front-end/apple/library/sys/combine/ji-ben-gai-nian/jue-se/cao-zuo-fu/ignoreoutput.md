# ignoreOutput

在 `Combine` 框架中，`ignoreOutput` 是一个操作符，用于忽略 `Publisher` 输出的所有值。这意味着你会启动 `Publisher` 的订阅，但其发出的任何值都将被忽略。`ignoreOutput` 适用于只关心 `Publisher` 是否完成或者发生错误，而不关心其输出的情况。

#### 基本用法

`ignoreOutput` 的签名如下：

```swift
func ignoreOutput() -> Publishers.IgnoreOutput<Self>
```

* **作用**: 它会创建一个新的 `Publisher`，该 `Publisher` 只会传递完成事件或错误事件，而不会传递任何数据。

#### 示例：忽略输出，只关心完成事件

假设我们有一个 `Publisher` 发出一些数据，我们可以使用 `ignoreOutput` 来忽略这些数据，只关心 `Publisher` 是否完成或发生错误。

```swift
import Combine

let numbers = [1, 2, 3, 4, 5].publisher

let ignoreOutputSubscription = numbers
    .ignoreOutput()  // 忽略所有输出的值
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Publisher finished.")  // 只会收到完成事件
            case .failure(let error):
                print("Error: \(error)")
            }
        },
        receiveValue: { value in
            print(value)  // 不会打印任何值，因为被忽略了
        }
    )
```

#### 输出结果

```
Publisher finished.
```

在这个示例中：

* 我们创建了一个 `Publisher`，它发出一系列数字。
* 通过 `ignoreOutput()` 操作符，我们忽略了所有这些数字，只关心 `Publisher` 是否完成。
* `sink` 接收并打印完成事件。

#### 示例：忽略输出，关心错误

假设我们有一个可能会失败的 `Publisher`，使用 `ignoreOutput` 可以仅关注错误事件，而不处理数据。

```swift
import Combine

enum CustomError: Error {
    case someError
}

let numbersWithError = [1, 2, 3].publisher

let errorHandlingSubscription = numbersWithError
    .ignoreOutput()  // 忽略所有输出的值
    .tryCatch { error -> AnyPublisher<Int, Error> in
        return Fail(outputType: Int.self, failure: CustomError.someError)
            .eraseToAnyPublisher()
    }
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Publisher finished.")
            case .failure(let error):
                print("Error: \(error)")  // 输出错误信息
            }
        },
        receiveValue: { value in
            print(value)  // 不会打印任何值，因为所有值都被忽略了
        }
    )
```

#### 输出结果

```
Error: someError
```

在这个示例中：

* 我们使用 `ignoreOutput()` 操作符来忽略 `Publisher` 输出的值。
* 然后，使用 `tryCatch` 操作符来模拟一个错误，并处理它。
* `sink` 接收并打印错误事件。

#### 使用场景

`ignoreOutput` 操作符常见的使用场景包括：

1. **只关心完成或错误事件**：如果你只需要知道一个操作是否成功完成，或是否失败，并不关心它发出的每个值，`ignoreOutput` 很有用。例如，进行一些后台操作时，只关心任务是否完成或失败。
2. **UI 更新控制**：有时你只关心某个事件的触发（如按钮点击），而不关心触发后返回的数据。例如，点击按钮时发送一个网络请求，你可能只关心请求的是否成功，而不关心请求返回的具体数据。
3. **简化数据流**：在某些情况下，你可能已经对数据进行了处理或过滤，只对操作的成功或失败结果感兴趣，使用 `ignoreOutput` 可以减少不必要的值处理。

#### 总结

* `ignoreOutput` 是一个简单而强大的操作符，用于忽略 `Publisher` 发出的所有输出。
* 通过它，你可以专注于 `Publisher` 的完成或错误事件，而不必处理每个发出的值。
* 它常用于只关心操作是否完成或是否失败的场景，尤其是在 UI 交互或后台任务处理中。
