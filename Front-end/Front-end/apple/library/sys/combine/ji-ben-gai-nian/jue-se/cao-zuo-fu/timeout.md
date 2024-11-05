# timeout

`timeout` 是 `Combine` 中的一个操作符，用于在指定的时间间隔内等待 `Publisher` 发出事件。如果在该时间间隔内没有收到任何事件，它将触发一个错误事件，表示超时。这对于处理可能没有按预期发出事件的情况非常有用，比如网络请求或其他异步操作。

#### `timeout` 的签名

```swift
func timeout(_ interval: Scheduler.TimeInterval, scheduler: Scheduler, customError: (() -> Failure)? = nil) -> Publishers.Timeout<Self>
```

* **`interval`**: 指定的时间间隔，表示等待事件的最长时间。
* **`scheduler`**: 控制事件调度的 `Scheduler`，例如 `DispatchQueue.main` 或 `RunLoop.main`。
* **`customError`**: 可选的自定义错误生成器，如果发生超时，可以用它来创建错误。

#### 工作原理

`timeout` 操作符会在指定的时间间隔内监测 `Publisher` 是否发出事件。如果超时，`timeout` 会发出一个错误事件（`failure`），并且不再接受任何值。

#### 示例：基本用法

以下示例展示了如何使用 `timeout` 操作符来处理可能超时的事件：

```swift
import Combine

let publisher = PassthroughSubject<Int, Never>()

let subscription = publisher
    .timeout(.seconds(2), scheduler: DispatchQueue.main) // 设置超时时间为 2 秒
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Publisher completed successfully.")
            case .failure(let error):
                print("Publisher timed out with error: \(error)")
            }
        },
        receiveValue: { value in
            print("Received value: \(value)")
        }
    )

// 在 3 秒后发送一个值（将导致超时）
DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
    publisher.send(1)
}

// 立即触发完成事件
DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    publisher.send(completion: .finished)
}
```

#### 输出结果：

```
Publisher timed out with error: Combine.Subscribers.Completion.failure
```

在这个示例中，由于在 2 秒的超时范围内没有值被发送，`timeout` 会触发一个错误事件，导致输出超时的错误信息。

#### 使用自定义错误

你可以通过 `customError` 参数为超时事件提供一个自定义错误：

```swift
import Combine

let publisher = PassthroughSubject<Int, Never>()

let timeoutError = NSError(domain: "CustomError", code: -1, userInfo: [NSLocalizedDescriptionKey: "Operation timed out."])

let subscription = publisher
    .timeout(.seconds(2), scheduler: DispatchQueue.main, customError: { timeoutError }) // 自定义超时错误
    .sink(
        receiveCompletion: { completion in
            switch completion {
            case .finished:
                print("Publisher completed successfully.")
            case .failure(let error):
                print("Publisher timed out with error: \(error.localizedDescription)")
            }
        },
        receiveValue: { value in
            print("Received value: \(value)")
        }
    )

// 在 3 秒后发送一个值（将导致超时）
DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
    publisher.send(1)
}
```

#### 输出结果：

```
Publisher timed out with error: Operation timed out.
```

在这个例子中，自定义的超时错误会被打印。

#### `timeout` 的注意事项

* **超时机制**：`timeout` 会监测整个 `Publisher` 的生命周期。如果在指定的时间间隔内没有发出任何事件，就会触发超时。
* **调度器**：选择合适的调度器来控制超时监测的行为，通常使用主线程以便于处理 UI 更新。
* **与其他操作符组合**：`timeout` 可以与其他操作符结合使用，例如在网络请求时等待响应。

#### 总结

* **`timeout`**：用于在指定时间间隔内等待 `Publisher` 发出事件，若未发出则触发超时错误。
* **适用场景**：处理网络请求、异步操作，确保操作在合理时间内完成。
* **自定义错误**：可以提供自定义错误信息以替代默认的超时错误。

通过适当地使用 `timeout`，可以确保应用程序在特定的时间内处理事件，避免因无响应或过长的延迟导致用户体验不佳。
