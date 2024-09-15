# 模板/泛型

在 Swift 中，模板类似于其他语言中的泛型（Generics）。泛型使代码更加灵活和可重用，可以编写适用于任意类型的函数、结构体、类和枚举。通过使用泛型，代码可以接受不同的数据类型，而不必为每个数据类型重复编写相同的逻辑。

#### 泛型的语法

**泛型函数**

泛型函数允许我们在函数中使用任意类型，而不局限于某一种特定类型。泛型类型通常以占位符形式表示，常见的形式是 `T`，但你也可以使用其他名字来表示类型占位符。

**示例：泛型函数**

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var x = 5
var y = 10
swapTwoValues(&x, &y)
print("x: \(x), y: \(y)")  // 输出：x: 10, y: 5

var a = "Hello"
var b = "World"
swapTwoValues(&a, &b)
print("a: \(a), b: \(b)")  // 输出：a: World, b: Hello
```

在这个例子中，`swapTwoValues` 函数能够交换任意类型的两个值，无论是整数、字符串还是其他类型。

**泛型类型（类、结构体和枚举）**

泛型不仅可以用于函数，也可以用于类、结构体和枚举，使其能够处理任意类型的数据。

**示例：泛型结构体**

```swift
struct Stack<Element> {
    var items: [Element] = []
    
    mutating func push(_ item: Element) {
        items.append(item)
    }
    
    mutating func pop() -> Element? {
        return items.popLast()
    }
}

var intStack = Stack<Int>()
intStack.push(1)
intStack.push(2)
print(intStack.pop()!)  // 输出：2

var stringStack = Stack<String>()
stringStack.push("A")
stringStack.push("B")
print(stringStack.pop()!)  // 输出：B
```

在这个例子中，`Stack` 结构体是一个泛型栈，它可以存储任意类型的元素，`Element` 是类型占位符。可以创建一个整数栈或字符串栈等。

**泛型类型约束**

有时候，你可能希望泛型只能作用于某些特定类型。例如，你希望某个泛型只能是遵循某个协议的类型，或者必须是某个特定类型的子类。

**示例：使用类型约束**

```swift
func findIndex<T: Equatable>(of valueToFind: T, in array: [T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}

let array = [1, 2, 3, 4, 5]
if let index = findIndex(of: 3, in: array) {
    print("Index of 3: \(index)")  // 输出：Index of 3: 2
}
```

在这个例子中，`T: Equatable` 是一个类型约束，它确保 `T` 类型必须遵循 `Equatable` 协议，也就是说该类型的实例可以进行相等比较。

**关联类型**

关联类型通常用于协议中，允许协议定义一个或多个占位符类型。这些占位符类型在协议实现时被具体化。

**示例：使用关联类型定义协议**

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct Stack<Element>: Container {
    var items: [Element] = []
    
    mutating func push(_ item: Element) {
        items.append(item)
    }
    
    mutating func pop() -> Element? {
        return items.popLast()
    }
    
    // Container 协议要求的实现
    mutating func append(_ item: Element) {
        self.push(item)
    }
    
    var count: Int {
        return items.count
    }
    
    subscript(i: Int) -> Element {
        return items[i]
    }
}
```

在这个例子中，`Container` 协议有一个关联类型 `Item`，`Stack` 结构体实现了这个协议，并将 `Item` 映射为 `Element`。

#### 泛型的优势

* **代码复用**：泛型允许编写通用代码，无需为每种类型编写不同版本的函数或类。
* **类型安全**：泛型确保代码在编译时进行类型检查，减少运行时错误。
* **灵活性和可扩展性**：可以为各种数据类型创建高效、灵活的算法和数据结构。

#### 总结

Swift 中的泛型提供了强大的功能，使得代码更加灵活和可重用。通过泛型函数、泛型类型以及类型约束，Swift 开发者可以编写适用于多种类型的高效代码，同时保持类型安全。泛型在 Swift 中是编写可扩展和通用代码的关键工具。
