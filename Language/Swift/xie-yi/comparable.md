# Comparable

在 Swift 中，`Comparable` 是一个协议，表示某种类型的实例可以进行比较。

遵守 `Comparable` 协议的类型可以通过特定的操作符进行排序和比较，比如 `<`、`<=`、`>` 和 `>=`。

这对于实现**排序算法、堆、优先队列**等数据结构非常有用。

#### `Comparable` 协议的定义：

一个遵循 `Comparable` 的类型必须实现 `==` 和 `<` 两个操作符。之后，其他比较操作符（如 `>`、`<=` 等）会自动生成。

#### 协议定义：

```swift
protocol Comparable : Equatable {
    static func < (lhs: Self, rhs: Self) -> Bool
    // 其他比较运算符，如:
    // static func <= (lhs: Self, rhs: Self) -> Bool
    // static func > (lhs: Self, rhs: Self) -> Bool
    // static func >= (lhs: Self, rhs: Self) -> Bool
}
```

#### `Comparable` 适用场景：

* **排序**：当你需要对数组进行排序时，数组中的元素需要是 `Comparable` 类型。
* **数据结构**：如二叉搜索树、堆或优先队列等依赖于元素的比较关系。
* **过滤与查找**：可以根据元素的比较结果进行过滤和搜索操作。

#### 示例：

```swift
struct Person: Comparable {
    var name: String
    var age: Int

    static func < (lhs: Person, rhs: Person) -> Bool {
        return lhs.age < rhs.age
    }
    
    static func == (lhs: Person, rhs: Person) -> Bool {
        return lhs.age == rhs.age
    }
}

let person1 = Person(name: "Alice", age: 25)
let person2 = Person(name: "Bob", age: 30)

print(person1 < person2)  // true, 因为 25 < 30
```

在这个示例中，`Person` 结构体遵循了 `Comparable` 协议，并根据 `age` 属性来比较两个 `Person` 实例的大小。
