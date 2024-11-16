# 元组

在 Swift 中，**tuple（元组）** 是一种将多个值组合成一个单一复合值的数据结构。元组可以包含多种类型的值，并且这些值的数量和类型不需要相同。

### 特性

* 元组是<mark style="color:red;">**固定大小**</mark>的。
* 元组内的<mark style="color:red;">元素类型可以不同</mark>。
* 元组可以用来<mark style="color:red;">返回多个值</mark>，特别适合从函数中返回多个相关值。

### 创建元组

你可以用圆括号 `()` 来创建元组：

```swift
let tuple1 = (1, "Hello", true) // 一个包含 Int、String 和 Bool 的元组
let tuple2: (Int, String) = (42, "Swift") // 明确指定元组类型
```

### 访问元组的值

1.  **通过索引访问**： 元组的值可以通过位置索引访问，索引从 `0` 开始。

    ```swift
    let myTuple = (1, "Swift", 3.14)
    print(myTuple.0) // 输出 1
    print(myTuple.1) // 输出 "Swift"
    print(myTuple.2) // 输出 3.14
    ```
2.  **通过命名访问**： 你可以为元组中的元素指定名字，以便更直观地访问。

    ```swift
    let person = (name: "Alice", age: 25)
    print(person.name) // 输出 "Alice"
    print(person.age)  // 输出 25
    ```

### 元组的解构

可以将元组分解成单独的变量：

```swift
let coordinates = (x: 10, y: 20)
let (x, y) = coordinates
print(x) // 输出 10
print(y) // 输出 20

// 如果不需要某个值，可以使用下划线 `_` 忽略它：
let (onlyX, _) = coordinates
print(onlyX) // 输出 10
```

### 使用场景

#### 1. <mark style="color:red;">返回多个值</mark>

元组通常用作函数返回多个值的一种方式。

```swift
func getUserInfo() -> (name: String, age: Int) {
    return ("Alice", 25)
}

let userInfo = getUserInfo()
print(userInfo.name) // 输出 "Alice"
print(userInfo.age)  // 输出 25
```

#### 2. <mark style="color:red;">暂时组合值</mark>

可以将多个值临时组合成一个元组，而不需要定义专门的结构体或类。

```swift
let point = (x: 3, y: 4)
print("Point is at (\(point.x), \(point.y))")
```

### 元组与数组的区别

| 特性    | 元组               | 数组                |
| ----- | ---------------- | ----------------- |
| 类型    | 可以包含不同类型的值       | 必须是相同类型的值         |
| 长度    | 固定               | 可变（通常使用 `var` 修饰） |
| 用途    | 适合表示一组相关的、固定数量的值 | 适合存储同类型的值的集合      |
| 可命名元素 | 支持               | 不支持               |



