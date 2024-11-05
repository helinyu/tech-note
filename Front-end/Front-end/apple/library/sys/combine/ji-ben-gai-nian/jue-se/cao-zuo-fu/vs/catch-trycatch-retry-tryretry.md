# catch、tryCatch、retry 、tryRetry

以下是 `Combine` 中的 `catch`、`tryCatch`、`retry` 和 `tryRetry` 操作符的对比表，概述了它们的功能、适用场景和行为：

| 操作符          | 功能描述                                           | 行为                                         | 适用场景           | 关键参数               |
| ------------ | ---------------------------------------------- | ------------------------------------------ | -------------- | ------------------ |
| **catch**    | 捕获并处理错误，允许提供替代的 `Publisher`                    | 当原始 `Publisher` 发送错误时，可以返回一个新的 `Publisher` | 网络请求失败、数据处理错误  | `handler`: 处理错误的闭包 |
| **tryCatch** | 捕获并处理错误，允许提供替代的 `Publisher`，并支持抛出错误            | 类似于 `catch`，但可以处理抛出的错误                     | 需要抛出错误的异步操作    | `handler`: 处理错误的闭包 |
| **retry**    | 当 `Publisher` 发送错误时，重新订阅原始 `Publisher`         | 可以指定重试次数，若失败则触发错误                          | 网络请求重试、操作失败后再试 | `times`: 重试次数      |
| **tryRetry** | 当 `Publisher` 发送错误时，重新订阅原始 `Publisher`，并支持抛出错误 | 类似于 `retry`，但可以处理抛出的错误                     | 需要抛出错误的重试操作    | `times`: 重试次数      |

#### 详细说明：

* **catch**：当 `Publisher` 遇到错误时，使用 `catch` 可以捕获错误并返回一个新的 `Publisher` 作为替代，适合处理错误并提供用户友好的反馈。
* **tryCatch**：类似于 `catch`，但可以捕获并处理抛出的错误，适用于需要在错误处理过程中进行异常处理的场景。
* **retry**：适用于希望在发生错误时自动重试原始操作的场景，例如在网络请求失败后尝试重新连接。
* **tryRetry**：与 `retry` 类似，但可以处理在重试过程中可能抛出的错误，适合更复杂的重试逻辑。

#### 示例用法

**catch**

```swift
let publisher = Fail<Int, Error>(error: NSError(domain: "", code: -1, userInfo: nil))

let subscription = publisher
    .catch { error in
        Just(0) // 返回一个默认值
    }
    .sink(receiveCompletion: { print($0) }, receiveValue: { print($1) }) 
```

**tryCatch**

```swift
let publisher = Fail<Int, Error>(error: NSError(domain: "", code: -1, userInfo: nil))

let subscription = publisher
    .tryCatch { error -> AnyPublisher<Int, Never> in
        return Just(0).eraseToAnyPublisher() // 返回一个默认值
    }
    .sink(receiveCompletion: { print($0) }, receiveValue: { print($1) }) 
```

**retry**

```swift
let publisher = Fail<Int, Error>(error: NSError(domain: "", code: -1, userInfo: nil))

let subscription = publisher
    .retry(3) // 尝试重试 3 次
    .sink(receiveCompletion: { print($0) }, receiveValue: { print($1) }) 
```

**tryRetry**

```swift
let publisher = Fail<Int, Error>(error: NSError(domain: "", code: -1, userInfo: nil))

let subscription = publisher
    .tryRetry(3) // 尝试重试 3 次，并捕获抛出的错误
    .sink(receiveCompletion: { print($0) }, receiveValue: { print($1) }) 
```

#### 总结

* **catch** 和 **tryCatch**：用于处理错误并返回替代的 `Publisher`，前者处理简单的错误，后者支持抛出错误。
* **retry** 和 **tryRetry**：用于在发生错误时重试操作，前者适用于简单重试，后者支持在重试时捕获错误。

这个表格和示例可以帮助你更好地理解这些操作符的功能及其适用场景。
