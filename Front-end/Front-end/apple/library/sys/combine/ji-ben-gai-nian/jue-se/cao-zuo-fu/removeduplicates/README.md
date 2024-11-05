# removeDuplicates

在 `Combine` 框架中，`removeDuplicates` 是一个用于移除连续重复值的操作符。它可以避免重复的值传递给下游订阅者，从而减少不必要的处理和更新。`removeDuplicates` 常用于只需要处理唯一值或非重复事件的场景，例如防止 UI 的频繁更新等。

#### 基本用法

`removeDuplicates` 的基本签名如下：

```swift
func removeDuplicates(by predicate: @escaping (Output, Output) -> Bool) -> Publishers.RemoveDuplicates<Self>
```

* **`predicate`**：一个可选的闭包，用于判断两个值是否相等。如果未提供该闭包，则会使用默认的相等性比较（前提是数据类型符合 `Equatable` 协议）。

当值类型符合 `Equatable` 时，可以直接使用默认的 `removeDuplicates()`，否则需要提供一个自定义的比较闭包。

#### 示例：默认用法

以下示例展示了 `removeDuplicates` 的基本用法。这里的 `Publisher` 是一组整数，其中一些值是连续重复的，`removeDuplicates` 会移除这些重复项：

```swift
import Combine

let numbers = [1, 1, 2, 2, 3, 3, 3, 4, 5, 5].publisher

let removeDuplicatesSubscription = numbers
    .removeDuplicates()
    .sink { value in
        print(value) // 输出: 1, 2, 3, 4, 5
    }
```

在这个示例中：

* 我们创建了一个包含整数的 `Publisher`。
* 使用 `removeDuplicates()` 去掉了相邻的重复值。
* `sink` 接收并打印过滤后的结果。

#### 示例：自定义比较闭包

当数据类型不符合 `Equatable` 协议，或者需要自定义的比较逻辑时，可以提供一个闭包。以下示例展示了如何使用 `removeDuplicates` 根据自定义规则过滤重复值：

```swift
struct User {
    let id: Int
    let name: String
}

let users = [
    User(id: 1, name: "Alice"),
    User(id: 1, name: "Alice"),
    User(id: 2, name: "Bob"),
    User(id: 2, name: "Bob"),
    User(id: 3, name: "Charlie")
].publisher

let customRemoveDuplicatesSubscription = users
    .removeDuplicates { previous, current in
        previous.id == current.id // 使用自定义的条件: 仅当 ID 相同时视为重复
    }
    .sink { user in
        print("User ID: \(user.id), Name: \(user.name)")
    }

// 输出:
// User ID: 1, Name: Alice
// User ID: 2, Name: Bob
// User ID: 3, Name: Charlie
```

在这个示例中：

* 我们创建了一个包含 `User` 对象的 `Publisher`。
* 使用 `removeDuplicates` 根据用户的 `id` 进行去重。
* `sink` 接收并打印过滤后的 `User` 对象。

#### 使用场景

`removeDuplicates` 适用于以下场景：

1. **减少重复更新**：在 UI 层中，减少不必要的重复更新。例如，只在数据有变化时更新视图。
2. **避免频繁事件触发**：在事件驱动的系统中，避免对同一事件的重复响应。
3. **过滤相邻重复值**：用于仅处理不连续的变化。

#### 注意事项

* `removeDuplicates` 仅移除**相邻**重复的值。如果重复的值不连续，它们依然会被发送到下游。
* 当处理非 `Equatable` 类型的数据时，需要提供自定义的比较闭包。

#### 示例：只移除相邻重复值

```swift
let repeatedNumbers = [1, 2, 2, 3, 1, 1, 4].publisher

let adjacentRemoveDuplicatesSubscription = repeatedNumbers
    .removeDuplicates()
    .sink { value in
        print(value) // 输出: 1, 2, 3, 1, 4
    }
```

在这个示例中：

* `removeDuplicates()` 仅移除了相邻的重复值 `2` 和 `1`，而未移除前后分隔的重复 `1`。

#### 总结

* `removeDuplicates` 是一个有效的去重工具，适用于需要移除相邻重复值的场景。
* 可以使用默认的相等性比较，也可以提供自定义的比较逻辑。
* 它适合用于减少不必要的事件响应，特别是避免 UI 更新或事件触发的重复处理。
