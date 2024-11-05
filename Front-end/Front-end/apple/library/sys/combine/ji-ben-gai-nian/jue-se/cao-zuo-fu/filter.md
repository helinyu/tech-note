# filter

在 `Combine` 框架中，`filter` 是一个用于筛选数据流中的值的操作符。它允许你根据条件判断是否允许一个值通过流，从而只让满足条件的值继续流向下游。

#### 基本用法

`filter` 的基本签名如下：

```swift
func filter(_ isIncluded: @escaping (Output) -> Bool) -> Publishers.Filter<Self>
```

* **`isIncluded`**: 一个闭包，接收当前的输入值并返回一个布尔值。如果返回 `true`，该值会继续传递到下游；如果返回 `false`，则会被过滤掉。

#### 示例

以下是一个简单的示例，将一组整数中过滤出偶数：

```swift
import Combine

let numbers = [1, 2, 3, 4, 5, 6].publisher

let filterSubscription = numbers
    .filter { number in
        number % 2 == 0 // 只允许偶数通过
    }
    .sink { value in
        print(value) // 输出: 2, 4, 6
    }
```

在这个示例中：

* 我们创建了一个包含整数的 `Publisher`。
* 使用 `filter` 操作符，只允许偶数通过。
* `sink` 接收并打印过滤后的结果。

#### 使用场景

`filter` 操作符的常见使用场景包括：

1. **数据清理**：在数据流中删除不符合特定条件的值，例如删除所有为负的值。
2. **状态检查**：在 UI 数据流中，可以根据用户的交互状态来过滤不必要的事件。
3. **权限控制**：根据用户权限或条件，限制某些数据或事件的传递。

#### 结合其他操作符使用

`filter` 可以与其他操作符（如 `map`、`compactMap` 等）结合使用，以创建更复杂的数据流。例如，你可以先使用 `filter` 过滤掉不需要的值，然后使用 `map` 进行转换。

```swift
let numbers = [1, 2, 3, 4, 5, 6].publisher

let filterAndMapSubscription = numbers
    .filter { $0 % 2 == 0 }  // 过滤偶数
    .map { "Even number: \($0)" } // 转换为字符串
    .sink { value in
        print(value) // 输出: Even number: 2, Even number: 4, Even number: 6
    }
```

#### 与 `compactMap` 的对比

*   `filter` 和 `compactMap` 的主要区别在于：`filter` 根据条件直接过滤掉不符合条件的值，而 `compactMap` 则会移除所有 `nil` 值。`compactMap` 也可以用于转换数据类型。

    ```swift
    let values = ["1", "a", "3", "b"].publisher

    let compactMapSubscription = values
        .compactMap { Int($0) } // 试图将字符串转换为整数，失败则移除 nil
        .sink { print($0) } // 输出: 1, 3
    ```

#### 错误处理

`filter` 本身不进行错误处理。如果需要处理可能抛出错误的条件，可以使用 `tryFilter`。它的用法与 `filter` 类似，但可以在条件判断中抛出错误，并将错误传递给下游处理。

```swift
let numbersWithError = [1, 2, 3, 4, 5].publisher

let tryFilterSubscription = numbersWithError
    .tryFilter { number in
        if number == 3 {
            throw NSError(domain: "", code: 0, userInfo: [NSLocalizedDescriptionKey: "Error at number 3"])
        }
        return number % 2 == 0
    }
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Completed successfully.")
        case .failure(let error):
            print("Error: \(error.localizedDescription)")
        }
    }, receiveValue: { value in
        print(value)
    })

// 输出:
// 2
// Error: Error at number 3
```

在这个示例中：

* `tryFilter` 用于在 `filter` 条件判断中抛出错误。
* 当值为 `3` 时抛出错误，导致数据流提前结束。

#### 总结

* `filter` 是 `Combine` 中一个重要的操作符，用于根据条件筛选数据流中的值。
* 它适用于数据清理、状态检查、权限控制等场景。
* `tryFilter` 是 `filter` 的变体，支持在条件判断中抛出错误。
* 结合 `filter` 和其他操作符可以创建复杂的数据流，帮助在数据流中筛选和转换符合条件的值。
