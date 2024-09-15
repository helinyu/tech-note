# 数组

Swift 中的数组（`Array`）是有序的、可重复的元素集合，存储相同类型的多个值。数组的功能非常丰富，包括创建、添加、修改、遍历、排序等。下面详细介绍 Swift 中数组的使用方法及操作内容。

#### 1. 数组的声明和初始化

**空数组**

可以通过指定元素类型创建一个空数组。

```swift
var emptyArray: [Int] = []  // 空的 Int 数组
```

或者使用构造器：

```swift
var anotherEmptyArray = Array<Int>()  // 空的 Int 数组
```

**带初始值的数组**

你可以通过直接声明数组并赋值：

```swift
var numbers = [1, 2, 3, 4]  // 这是一个包含4个元素的数组
```

**重复某个值的数组**

使用指定数量的重复值来初始化数组：

```swift
var repeatedArray = Array(repeating: 0, count: 5)  // [0, 0, 0, 0, 0]
```

#### 2. 访问和修改数组

**访问数组元素**

通过下标（索引）访问数组的元素。数组索引从 `0` 开始。

```swift
let firstElement = numbers[0]  // 访问第一个元素，值为 1
```

**修改数组元素**

可以通过下标直接修改数组中的元素：

```swift
numbers[1] = 10  // 修改数组中索引为1的元素，数组变为 [1, 10, 3, 4]
```

**添加元素**

* **在数组末尾添加元素**：

```swift
numbers.append(5)  // 数组变为 [1, 10, 3, 4, 5]
```

* **添加多个元素**：

```swift
numbers += [6, 7]  // 数组变为 [1, 10, 3, 4, 5, 6, 7]
```

* **在指定位置插入元素**：

```swift
numbers.insert(0, at: 0)  // 在索引0处插入0，数组变为 [0, 1, 10, 3, 4, 5, 6, 7]
```

**移除元素**

* **移除特定位置的元素**：

```swift
let removedElement = numbers.remove(at: 2)  // 移除索引2处的元素，数组变为 [0, 1, 3, 4, 5, 6, 7]
```

* **移除最后一个元素**：

```swift
numbers.removeLast()  // 移除最后一个元素，数组变为 [0, 1, 3, 4, 5, 6]
```

* **移除所有元素**：

```swift
numbers.removeAll()  // 清空数组
```

**检查数组是否为空**

```swift
if numbers.isEmpty {
    print("Array is empty")
}
```

#### 3. 遍历数组

**使用 `for-in` 循环遍历**

```swift
for number in numbers {
    print(number)
}
```

**使用 `enumerated()` 获取索引和元素**

```swift
for (index, value) in numbers.enumerated() {
    print("Item \(index): \(value)")
}
```

#### 4. 数组的常用属性和方法

* **`count`**：返回数组中的元素数量。

```swift
let count = numbers.count  // 数组中元素的个数
```

* **`first` 和 `last`**：访问数组的第一个和最后一个元素。

```swift
let firstElement = numbers.first  // 可选类型，返回数组的第一个元素
let lastElement = numbers.last  // 可选类型，返回数组的最后一个元素
```

* **`contains(_:)`**：检查数组是否包含某个元素。

```swift
let hasValue = numbers.contains(4)  // 返回 true，如果数组中包含元素 4
```

* **`sorted()`**：返回排序后的数组，不改变原数组。

```swift
let sortedNumbers = numbers.sorted()  // 升序排列
```

* **`reverse()`**：反转数组元素顺序。

```swift
numbers.reverse()  // 原地反转数组
```

#### 5. 多维数组

Swift 中也支持多维数组，比如二维数组。你可以创建包含数组的数组。

```swift
var matrix: [[Int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix[1][2])  // 访问第二行第三列，输出 6
```

#### 6. 数组的类型安全与可变性

* **类型安全**：Swift 的数组是类型安全的，也就是说它只能存储指定类型的元素。例如，如果你声明了一个 `Int` 类型的数组，那么只能在这个数组中添加整数。

```swift
var intArray: [Int] = [1, 2, 3]
// intArray.append("hello")  // 错误，不能添加非整数类型
```

* **可变性**：通过 `var` 定义的数组是可变的，可以修改、添加、删除元素。通过 `let` 定义的数组是不可变的，无法对其进行修改。

```swift
let constantArray = [1, 2, 3]
// constantArray.append(4)  // 错误，不可变数组不能修改
```

#### 7. 数组的高阶函数

Swift 提供了许多有用的高阶函数来操作数组，比如 `map`、`filter`、`reduce` 等。

**`map(_:)`**

`map` 方法通过将闭包作用于数组的每个元素，生成一个新数组。

```swift
let squaredNumbers = numbers.map { $0 * $0 }  // 每个元素平方
```

**`filter(_:)`**

`filter` 方法通过给定的条件过滤数组，返回一个满足条件的元素数组。

```swift
let evenNumbers = numbers.filter { $0 % 2 == 0 }  // 过滤出偶数
```

**`reduce(_:_:)`**

`reduce` 方法将数组中的元素组合为一个值。

```swift
let sum = numbers.reduce(0, +)  // 计算数组元素的总和
```

#### 总结

Swift 中的数组是强大的集合类型，支持多种操作，如添加、修改、删除、排序、过滤等。它们提供了良好的类型安全和性能，并且在实际开发中广泛应用。通过高阶函数、遍历和多维数组的支持，Swift 数组可以处理各种复杂的数据结构和算法场景。
