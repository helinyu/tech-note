# Equatable

在 Swift 中，`Equatable` 是一个协议，用于表示一种类型的实例可以进行**相等性比较**。

任何遵循 `Equatable` 协议的类型，都需要实现 `==` 和 `!=` 操作符，从而能够判断两个实例是否相等或不相等。

#### `Equatable` 协议的定义：

```swift
protocol Equatable {
    static func == (lhs: Self, rhs: Self) -> Bool
}
```

遵循 `Equatable` 协议的类型必须实现 `==` 操作符，以定义两个对象何时视为相等。`!=` 操作符是通过 `==` 自动推导的，因此只要实现了 `==`，系统会自动为你提供 `!=` 的功能。

#### 作用：

`Equatable` 主要用于类型实例的比较，这在以下情况下非常有用：

* **数组的查找**：例如使用 `contains` 或 `index(of:)` 方法时，数组元素需要是 `Equatable` 类型。
* **集合操作**：如字典中的键或集合中的元素，需要比较相等性。
* **条件判断**：实现对象相等性判断的类或结构体。

#### 示例：

```swift
struct Person: Equatable {
    var name: String
    var age: Int
    
    static func == (lhs: Person, rhs: Person) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age
    }
}

let person1 = Person(name: "Alice", age: 25)
let person2 = Person(name: "Alice", age: 25)
let person3 = Person(name: "Bob", age: 30)

print(person1 == person2)  // true
print(person1 == person3)  // false
```

在这个示例中，`Person` 结构体实现了 `Equatable`，根据 `name` 和 `age` 属性来判断两个 `Person` 实例是否相等。由于 `person1` 和 `person2` 的属性值相同，它们被认为是相等的。
