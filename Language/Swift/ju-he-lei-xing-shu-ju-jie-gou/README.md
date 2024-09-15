# 聚合类型数据结构

Swift 中有几种常见的容器数据结构，它们用于存储多个值。每种数据结构都有特定的特性和用途。主要的容器数据结构包括：`Array`（数组）、`Set`（集合）、`Dictionary`（字典）和 `Tuple`（元组）。下面我们来详细介绍每种容器数据结构。

#### 1. 数组（Array）

`Array` 是一个有序的、可重复的集合，存储相同类型的多个值。数组可以按顺序存储元素，并通过索引访问。

**特性：**

* 有序：元素存储的顺序就是它们的排列顺序。
* 可重复：同一个值可以在数组中出现多次。
* 通过索引访问元素，索引从 `0` 开始。

**示例：**

```swift
var numbers: [Int] = [1, 2, 3, 4]
numbers.append(5)  // 添加元素
print(numbers[0])  // 访问第一个元素，输出 1
```

**适用场景：**

适合需要存储多个有序且可能重复的数据的情况，比如处理列表、队列等。

#### 2. 集合（Set）

`Set` 是一个无序的、唯一的集合，存储相同类型的多个值。集合中的每个值都是唯一的，没有重复的元素。

**特性：**

* 无序：元素在集合中的排列没有固定顺序。
* 唯一：集合中的所有元素都是唯一的，不允许重复元素。
* 通过哈希值快速查找元素。

**示例：**

```swift
var fruits: Set<String> = ["Apple", "Banana", "Orange"]
fruits.insert("Mango")  // 添加元素
print(fruits.contains("Apple"))  // 检查集合是否包含某个元素，输出 true
```

**适用场景：**

适合需要存储唯一元素的情况，比如存储不重复的 ID、集合运算（交集、并集、差集）等。

#### 3. 字典（Dictionary）

`Dictionary` 是一个无序的、键值对（`key-value`）集合。每个键是唯一的，并与一个特定的值相关联。字典中的键和值必须是相同类型的。

**特性：**

* 无序：键值对的排列顺序不确定。
* 唯一键：字典中的键必须唯一，每个键只能映射到一个值。
* 键和值都可以是任意类型，但必须是同一种类型。

**示例：**

```swift
var studentScores: [String: Int] = ["Alice": 90, "Bob": 85]
studentScores["Charlie"] = 92  // 添加或更新键值对
print(studentScores["Alice"]!)  // 访问字典中的值，输出 90
```

**适用场景：**

适合需要存储键值对的情况，比如通过名字查找电话号码、通过 ID 查找信息等。

#### 4. 元组（Tuple）

`Tuple` 是一组值的集合，存储多个不同类型的值。与数组和集合不同，元组可以存储不同类型的数据，且元素的数量和类型是固定的。

**特性：**

* 有序：元组的元素有固定顺序。
* 固定大小：元组的元素数量和类型在定义时固定，不可更改。
* 可以包含不同类型的值。

**示例：**

```swift
let person: (String, Int) = ("Alice", 25)
print(person.0)  // 访问元组中的第一个元素，输出 "Alice"
print(person.1)  // 访问元组中的第二个元素，输出 25
```

**适用场景：**

适合临时存储一组相关的值，但不需要创建一个专门的数据结构，比如函数返回多个值时。

#### 5. 可选集（Option Set）

`OptionSet` 是一个表示位掩码的集合，常用于表示一组相关的选项。每个选项在底层都由一个二进制位来表示。

**特性：**

* 用于表示一组选项或标志。
* 每个选项是通过位掩码实现的，因此可以使用位运算进行操作。

**示例：**

```swift
struct Directions: OptionSet {
    let rawValue: Int
    static let north = Directions(rawValue: 1 << 0)
    static let south = Directions(rawValue: 1 << 1)
    static let east  = Directions(rawValue: 1 << 2)
    static let west  = Directions(rawValue: 1 << 3)
}

let travelDirection: Directions = [.north, .east]
```

**适用场景：**

适合表示选项或标志的集合，比如用户权限、系统配置标志等。

#### 6. 其他容器数据结构

**- `IndexSet`**

`IndexSet` 是 `Set` 的一个变体，用于存储无符号整数（`UInt`）的集合，常用于存储一组索引值。

**示例：**

```swift
var indexSet: IndexSet = [1, 2, 3, 5]
indexSet.insert(10)
print(indexSet)  // 输出 [1, 2, 3, 5, 10]
```

**- `OrderedSet`**

Swift 目前没有内置的 `OrderedSet`（有序集合），但是你可以使用 `Foundation` 框架提供的 `NSOrderedSet`，或者使用第三方库实现。`OrderedSet` 结合了数组和集合的特性，既有序又唯一。

#### 总结

Swift 提供了多种容器数据结构，以满足不同场景下的需求：

* **`Array`**：有序、可重复的集合。
* **`Set`**：无序、唯一的集合。
* **`Dictionary`**：无序的键值对集合。
* **`Tuple`**：固定大小、可以包含不同类型的有序集合。
* **`OptionSet`**：位掩码选项集合，常用于标志操作。
* **`IndexSet`** 和 `OrderedSet`：用于存储索引的集合，以及有序的唯一集合。

每种容器数据结构都有其特定的用途和操作方式，可以根据具体需求选择合适的数据结构。
