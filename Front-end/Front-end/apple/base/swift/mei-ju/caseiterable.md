# CaseIterable

`CaseIterable` 是 Swift 提供的一个协议，<mark style="color:red;">**用来自动为枚举类型生成一个包含所有枚举值的集合**</mark>。它适用于只有 `enum` 才能采用的特性，即枚举中所有的可能值都可以被迭代。

通过让枚举类型遵循 `CaseIterable` 协议，Swift 会自动生成一个 `allCases` 属性，它包含该枚举的所有值，这使得你可以方便地遍历和访问这些值。

#### 语法

要使用 `CaseIterable`，只需让你的枚举遵循该协议：

```swift
enum SomeEnum: CaseIterable {
    case first
    case second
    case third
}
```

#### 自动生成的 `allCases` 属性

当枚举遵循 `CaseIterable` 时，Swift 自动为其提供一个 `allCases` 的静态属性，返回一个包含所有枚举值的数组：

```swift
for value in SomeEnum.allCases {
    print(value)
}
```

输出：

```
first
second
third
```

#### 适用场景

1. **迭代枚举值**：当你需要遍历所有可能的枚举值时，`CaseIterable` 非常有用。比如，用户界面上展示一组选项、测试用例、数据序列化/反序列化等。
2. **减少手动维护**：如果没有 `CaseIterable`，你需要手动维护一个所有枚举值的数组，而 `CaseIterable` 自动生成这个数组，避免了错误和维护成本。

#### 示例

```swift
enum Direction: CaseIterable {
    case north
    case south
    case east
    case west
}

for direction in Direction.allCases {
    print(direction)
}
```

输出：

```
north
south
east
west
```

#### 自定义 `allCases`（在复杂场景下）

虽然 Swift 会自动为 `CaseIterable` 提供默认的 `allCases`，但你也可以为复杂的枚举自定义 `allCases` 属性。例如，如果枚举有关联值，或者你不希望某些枚举值出现在 `allCases` 中，你可以手动实现：

```swift
enum Filter: CaseIterable {
    case byName
    case byDate
    case custom(String)

    static var allCases: [Filter] {
        return [.byName, .byDate] // 排除 .custom
    }
}
```

#### 总结

* **`CaseIterable`** 协议让你可以轻松地获得所有枚举值，特别适用于没有关联值的简单枚举。
* 通过 `allCases` 属性，可以遍历枚举的所有可能值，减少手动维护的错误风险。
