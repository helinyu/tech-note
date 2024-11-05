# map

在 `Combine` 框架中，`map` 是一个常用的操作符，用于将 `Publisher` 发出的值转换为其他类型或格式。它通过接收一个闭包，将输入值转换为输出值，形成一个新的 `Publisher`。`map` 操作符对于数据处理和变换非常有用。

#### 基本用法

`map` 的基本签名如下：

```swift
func map<T>(_ transform: @escaping (Output) -> T) -> Publishers.Map<Self, T>
```

* **`transform`**: 一个闭包，接收输入值并返回转换后的输出值。

#### 示例

以下是一个使用 `map` 操作符的简单示例，将一组整数转换为字符串：

```swift
import Combine

let numbers = [1, 2, 3, 4, 5].publisher

let stringSubscription = numbers
    .map { number in
        "Number: \(number)"
    }
    .sink { stringValue in
        print(stringValue)
    }

// 输出:
// Number: 1
// Number: 2
// Number: 3
// Number: 4
// Number: 5
```

在这个示例中：

* 我们创建了一个包含数字的 `Publisher`。
* 使用 `map` 将每个数字转换为字符串格式。
* 通过 `sink` 接收并打印转换后的字符串。

#### 使用场景

`map` 操作符适用于以下场景：

1. **数据类型转换**：当你需要将一种数据类型转换为另一种类型时，例如将整数转换为字符串或将模型对象转换为字典。
2. **数据格式化**：在数据流中对输出值进行格式化，例如将日期转换为字符串格式。
3. **简化数据结构**：在处理复杂数据结构时，可以使用 `map` 将其转换为更简单的结构。

#### 示例：将模型对象转换为字典

以下示例展示如何使用 `map` 将自定义对象转换为字典：

```swift
struct User {
    let id: Int
    let name: String
}

let users = [
    User(id: 1, name: "Alice"),
    User(id: 2, name: "Bob")
].publisher

let userDictionarySubscription = users
    .map { user in
        ["id": user.id, "name": user.name] // 将 User 对象转换为字典
    }
    .sink { userDict in
        print(userDict)
    }

// 输出:
// ["id": 1, "name": "Alice"]
// ["id": 2, "name": "Bob"]
```

#### 使用 `map` 与其他操作符结合

`map` 可以与其他 `Combine` 操作符结合使用，以创建复杂的数据流处理。例如，你可以先使用 `map` 转换数据，然后使用 `filter` 过滤结果。

```swift
let numbers = [1, 2, 3, 4, 5].publisher

let filteredSubscription = numbers
    .map { number in
        number * 2 // 将每个数字乘以 2
    }
    .filter { doubledNumber in
        doubledNumber > 5 // 过滤大于 5 的数字
    }
    .sink { filteredValue in
        print(filteredValue)
    }

// 输出:
// 6
// 8
// 10
```

在这个示例中：

* 首先使用 `map` 将每个数字乘以 2。
* 然后使用 `filter` 只保留大于 5 的数字。

#### 错误处理

如果你的数据流可能会发生错误，可以使用 `tryMap` 替代 `map` 来处理潜在的错误。这允许你在转换过程中捕获并处理错误。

```swift
let numbersWithError = [1, 2, 3, 4, 5].publisher
    .tryMap { number -> String in
        if number == 4 {
            throw NSError(domain: "", code: 0, userInfo: [NSLocalizedDescriptionKey: "Error encountered!"])
        }
        return "Number: \(number)"
    }

let subscriptionWithErrorHandling = numbersWithError
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Completed successfully.")
        case .failure(let error):
            print("Error: \(error.localizedDescription)")
        }
    }, receiveValue: { stringValue in
        print(stringValue)
    })

// 输出:
// Number: 1
// Number: 2
// Number: 3
// Error: Error encountered!
```

在这个示例中：

* 使用 `tryMap` 可以在数字为 `4` 时抛出错误。
* 在 `sink` 的 `receiveCompletion` 闭包中处理错误并打印相应的信息。

#### 总结

* `map` 是 `Combine` 中的一个核心操作符，用于将 `Publisher` 发出的值转换为其他类型。
* 它适用于数据类型转换、数据格式化和简化数据结构等场景。
* `map` 可以与其他操作符结合使用，形成更复杂的数据流处理。
* 使用 `tryMap` 可以在转换过程中处理潜在的错误，提高数据处理的鲁棒性。
