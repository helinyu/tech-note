# map、trymap、compactMap flatMap

在 `Combine` 框架中，`map`、`tryMap`、`compactMap` 和 `flatMap` 是四个常用的操作符，它们都用于转换 `Publisher` 发出的值，但各自的用途和行为有所不同。以下是对这四个操作符的比较及其示例：

#### 1. `map`

* **用途**: 将每个输入值转换为另一个值。
* **返回值**: 新的类型。
* **错误处理**: 不处理错误，直接返回转换后的值。

**示例**

```swift
import Combine

let numbers = [1, 2, 3].publisher

let mapSubscription = numbers
    .map { number in
        number * 2 // 将每个数字乘以 2
    }
    .sink { value in
        print(value) // 输出: 2, 4, 6
    }
```

#### 2. `tryMap`

* **用途**: 类似于 `map`，但可以处理转换中的错误。
* **返回值**: 新的类型或抛出错误。
* **错误处理**: 处理错误并将其传递到下游。

**示例**

```swift
let numbersWithError = [1, 2, 3, 4].publisher

let tryMapSubscription = numbersWithError
    .tryMap { number -> Int in
        if number == 3 {
            throw NSError(domain: "", code: 0, userInfo: [NSLocalizedDescriptionKey: "Error at number 3"])
        }
        return number * 2
    }
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Completed successfully.")
        case .failure(let error):
            print("Error: \(error.localizedDescription)")
        }
    }, receiveValue: { value in
        print(value) // 输出: 2, 4
    })
// 输出: Error: Error at number 3
```

#### 3. `compactMap`

* **用途**: 将输入值转换为另一个值，并移除所有 `nil` 值。
* **返回值**: 新的类型，不包含 `nil`。
* **错误处理**: 不处理错误，忽略返回 `nil` 的情况。

**示例**

```swift
let mixedNumbers: [Int?] = [1, 2, nil, 4, nil]

let compactMapSubscription = mixedNumbers.publisher
    .compactMap { $0 } // 移除 nil 值
    .sink { value in
        print(value) // 输出: 1, 2, 4
    }
```

#### 4. `flatMap`

* **用途**: 将输入值转换为一个 `Publisher`，然后将所有输出扁平化为单一的流。
* **返回值**: 新的 `Publisher`。
* **错误处理**: 不处理错误，但可以在内层 `Publisher` 中处理。

**示例**

```swift
let numbersForFlatMap = [1, 2, 3].publisher

let flatMapSubscription = numbersForFlatMap
    .flatMap { number in
        Just(number * 2) // 将每个数字转换为新的 Publisher
    }
    .sink { value in
        print(value) // 输出: 2, 4, 6
    }
```

#### 总结对比表格

| 特性       | `map`   | `tryMap`          | `compactMap`   | `flatMap`                |
| -------- | ------- | ----------------- | -------------- | ------------------------ |
| **用途**   | 转换输入值   | 转换输入值并处理错误        | 转换并移除 `nil` 值  | 将输入值转换为 `Publisher` 并扁平化 |
| **返回值**  | 新的类型    | 新的类型或抛出错误         | 新的类型，不含 `nil`  | 新的 `Publisher`           |
| **错误处理** | 不处理错误   | 处理错误              | 不处理错误，忽略 `nil` | 依赖内层 `Publisher` 中的错误处理  |
| **输出示例** | 2, 4, 6 | Error at number 3 | 1, 2, 4        | 2, 4, 6                  |

通过这四个操作符，你可以在 `Combine` 中灵活地处理和转换数据流，以满足不同的需求。选择合适的操作符可以帮助你更有效地处理输入数据、处理潜在错误、移除无效数据或扁平化复杂的输出。
