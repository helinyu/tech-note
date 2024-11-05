# Scan

在 `Combine` 框架中，`scan` 是一个操作符，用于将 `Publisher` 发出的多个值累积到一个单一的输出值。与 `reduce` 类似，但 `scan` 允许在每个输入值被处理时发出中间结果，这样可以提供一个更为逐步的输出流。

#### `scan` 的基本用法

`scan` 的基本签名如下：

```swift
func scan<Result>(_ initialResult: Result, _ nextPartialResult: @escaping (Result, Output) -> Result) -> Publishers.Scan<Self, Result>
```

* **`initialResult`**: 初始值，用于开始累加。
* **`nextPartialResult`**: 一个闭包，接收当前的累加结果和下一个输入值，并返回更新后的结果。

#### 与 `reduce` 的区别

* **输出频率**：`scan` 在处理每个值时都会输出当前的累加结果，而 `reduce` 只在源 `Publisher` 完成时输出最终结果。
* **中间结果**：`scan` 适合需要在处理过程中查看中间状态的场景，而 `reduce` 更适合仅关心最终结果的场景。

#### 示例

以下是一个使用 `scan` 操作符的简单示例，用于计算一个数字序列的累积和，并在每次新数字到来时输出当前的累积和。

```swift
import Combine

let numbers = [1, 2, 3, 4, 5].publisher

let cumulativeSumSubscription = numbers
    .scan(0) { (currentSum, number) in
        currentSum + number
    }
    .sink { cumulativeSum in
        print("Cumulative sum: \(cumulativeSum)")
    }

// 输出:
// Cumulative sum: 1
// Cumulative sum: 3
// Cumulative sum: 6
// Cumulative sum: 10
// Cumulative sum: 15
```

在这个示例中：

* 我们创建了一个包含数字的 `Publisher`。
* 使用 `scan` 操作符，将初始值设置为 `0`，并定义了如何累加每个数字。
* 每当新的数字被接收到时，当前的累积和会被输出。

#### 使用场景

`scan` 操作符适用于以下场景：

1. **实时计算**：当你需要在数据流中计算实时结果时，例如逐步求和、逐步计数等。
2. **状态跟踪**：在状态管理中，可以用 `scan` 来跟踪状态的变化，并在每次变化时输出当前状态。
3. **动态数据转换**：将输入值逐步转化为其他数据结构，如累积数组、字符串拼接等。

#### 示例：状态跟踪

以下示例演示如何使用 `scan` 来跟踪状态的变化，例如在每次输入时更新一个计数器：

```swift
let events = ["click", "click", "hover", "click"].publisher

let clickCountSubscription = events
    .scan(0) { (clickCount, event) in
        event == "click" ? clickCount + 1 : clickCount
    }
    .sink { count in
        print("Click count: \(count)")
    }

// 输出:
// Click count: 1
// Click count: 2
// Click count: 2
// Click count: 3
```

在这个示例中：

* 我们创建了一个事件序列，模拟用户交互。
* 使用 `scan` 来计算“click”事件的数量，只有在“click”事件发生时，计数才会增加。
* 每次更新计数时，当前的计数都会被输出。

#### 示例：累积数组

你还可以使用 `scan` 来创建一个数组，其中包含所有接收到的值的累积结果：

```swift
let numberStream = [1, 2, 3, 4, 5].publisher

let accumulatedArraySubscription = numberStream
    .scan([]) { (accumulated, number) in
        accumulated + [number] // 每次接收到新数字时，将其添加到数组中
    }
    .sink { array in
        print("Accumulated array: \(array)")
    }

// 输出:
// Accumulated array: [1]
// Accumulated array: [1, 2]
// Accumulated array: [1, 2, 3]
// Accumulated array: [1, 2, 3, 4]
// Accumulated array: [1, 2, 3, 4, 5]
```

在这个示例中：

* `scan` 用于累积一个数组，输出每一步的结果。
* 每次新的数字到达时，都会输出包含所有接收到的数字的数组。

#### 总结

* `scan` 是 `Combine` 中的一个强大操作符，用于将多个输入值累积到一个单一的输出值，并在每个输入值被处理时输出当前的累积结果。
* 它适合于实时计算、状态跟踪和动态数据转换等场景。
* 通过使用 `scan`，你可以更灵活地处理数据流，并在需要时访问中间结果。
