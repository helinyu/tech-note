# throttle

`throttle` 是 `Combine` 中的一个操作符，用于限制事件的发出频率。与 `debounce` 不同，`throttle` 在指定的时间间隔内，强制每个时间段只发出一个事件。即使在这个时间段内收到了多个事件，`throttle` 也只会发出第一个事件，而忽略其余的事件，直到下一个时间段结束。

#### `throttle` 的签名

```swift
func throttle(for: Scheduler.TimeInterval, scheduler: Scheduler) -> Publishers.Throttle<Self>
```

* **`for`**: 指定的时间间隔，表示在这个时间段内只允许发出一个事件。
* **`scheduler`**: 控制事件调度的 `Scheduler`，例如 `DispatchQueue.main` 或 `RunLoop.main`。

#### 工作原理

`throttle` 在指定的时间间隔内只发出第一个接收到的事件。时间间隔结束后，接下来的事件将在下一个时间段内发出。此操作符常用于处理高频率事件，比如按钮点击或滚动事件，以避免过于频繁的事件处理。

#### 示例：基本用法

以下示例展示了如何使用 `throttle` 操作符限制事件的频率：

```swift
import Combine

let publisher = PassthroughSubject<Int, Never>()

let subscription = publisher
    .throttle(for: .seconds(1), scheduler: DispatchQueue.main, latest: true) // 每秒发出一个事件
    .sink { value in
        print("Received value: \(value)")
    }

// 模拟快速发送值
publisher.send(1)
publisher.send(2)
DispatchQueue.main.asyncAfter(deadline: .now() + 0.5) {
    publisher.send(3) // 在 1 秒内，这个值会被忽略
}
DispatchQueue.main.asyncAfter(deadline: .now() + 1.5) {
    publisher.send(4) // 1 秒后会发出这个值
}
DispatchQueue.main.asyncAfter(deadline: .now() + 2.5) {
    publisher.send(5) // 1 秒后会发出这个值
}
```

#### 输出结果（每秒发出一个值）：

```
Received value: 1
Received value: 4
Received value: 5
```

在这个示例中，`publisher` 发出的事件在 1 秒内只会发出第一个值（`1`），后续在同一秒内的值（`3`）会被忽略。然后，在 1.5 秒和 2.5 秒后会分别发出值（`4` 和 `5`）。

#### `throttle` 与调度器

`throttle` 操作符需要一个调度器（`scheduler`）来指定事件的调度行为。常见的调度器包括：

* **`DispatchQueue`**: 指定在主线程或后台线程上处理事件。
* **`RunLoop`**: 用于基于运行循环的调度，适合与 UI 相关的操作。

#### 使用 `throttle` 处理用户输入

`throttle` 特别适合处理用户输入事件，如按钮点击：

```swift
import Combine

let buttonPublisher = PassthroughSubject<Void, Never>()

let subscription = buttonPublisher
    .throttle(for: .seconds(2), scheduler: DispatchQueue.main) // 每 2 秒触发一次
    .sink {
        print("Button tapped!")
    }

// 模拟快速点击按钮
buttonPublisher.send() // 第一次点击
buttonPublisher.send() // 第二次点击
DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    buttonPublisher.send() // 第三次点击（会被忽略）
}
DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
    buttonPublisher.send() // 第四次点击（会被处理）
}
```

#### 输出结果（每 2 秒发出一次）：

```
Button tapped!
```

在这个示例中，尽管按钮被快速点击多次，只有第一次点击会在 2 秒后被处理，后续的点击事件会被忽略，直到 2 秒过去后才能处理下一次点击。

#### `throttle` 的注意事项

* **发出事件的数量**：`throttle` 仅在指定的时间间隔内发出第一个接收到的事件，其他事件会被忽略。
* **是否发出最后一个事件**：`throttle` 可以设置参数 `latest` 来控制是否在时间段结束时发出最后一个接收到的事件。`latest: true` 表示在时间段结束时发出最后一个事件，`latest: false` 则不发出。
* **与其他操作符组合**：`throttle` 可以与其他操作符组合使用，增加流控制的灵活性。

#### 总结

* **`throttle`**：用于限制流中事件的发出频率，确保在指定时间段内只处理第一个事件。
* **适用场景**：按钮点击、滚动事件、输入框内容更新等需要降低事件频率的场景。
* **调度器**：可指定在哪个调度器上执行调度，通常选择主线程以处理 UI 更新。

通过适当地使用 `throttle`，可以有效地控制高频率事件的处理，避免不必要的性能损失和逻辑错误。
