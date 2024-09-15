---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 字符串(字符)

### 前提：

swift中不用过多关注字符，应该基于字符串来处理文本。



在 Swift 中，**字符串（String）** 是一种用于存储和操作文本的数据类型。Swift 的字符串是 Unicode 兼容的，因此可以处理多种语言的字符，并且具备很强的灵活性和安全性。



## 1. **声明与初始化字符串**

字符串可以通过字面量直接声明和初始化，使用 **双引号** 包裹文本：

```swift
let greeting = "Hello, world!"
```

还可以使用 `String` 的构造器进行初始化：

```swift
let anotherGreeting = String("Hi there!")
```

## 2. **字符（Character）类型**

Swift 中，字符（`Character`）是单个 Unicode 字符，使用双引号来表示。例如：

```swift
let char: Character = "A"
```

可以通过遍历字符串来获取字符：

```swift
for letter in greeting {
    print(letter)
}
```

## 3. **字符串插值**

Swift 支持 **字符串插值**，允许将变量或表达式嵌入到字符串中：

```swift
let name = "John"
let message = "Hello, \(name)!"
```

插值通过 `\()` 的形式实现，非常适合将变量的值直接插入到字符串中。

## 4. **字符串的拼接**

可以使用加号 (`+`) 进行字符串的拼接：

```swift
let part1 = "Hello, "
let part2 = "Swift!"
let combined = part1 + part2
```

或者使用 `+=` 将一个字符串追加到另一个字符串上：

```swift
var message = "Hello"
message += ", World!"
```

## 5. **字符串的常见操作**

*   **判断是否为空**: 使用 `isEmpty` 属性。

    ```swift
    if greeting.isEmpty {
        print("The string is empty")
    }
    ```
*   **获取字符串长度**: 使用 `count` 属性。

    ```swift
    print("The string has \(greeting.count) characters")
    ```
*   **访问字符串的字符**: 通过下标或 `startIndex` 等方式。

    ```swift
    let firstLetter = greeting[greeting.startIndex]
    ```
*   **修改字符串**: 可以插入、删除或替换字符。

    ```swift
    var welcome = "Hello"
    welcome.insert("!", at: welcome.endIndex)
    ```

## 6. **多行字符串字面量**

Swift 支持多行字符串，可以使用三对双引号 (`"""`) 来声明多行字符串：

```swift
let multilineString = """
This is a
multiline string in Swift.
"""
```

## 7. **字符串的可变与不可变**

默认情况下，使用 `let` 声明的字符串是不可变的（immutable），不能修改。要修改字符串，必须使用 `var` 声明：

```swift
var mutableString = "Change me"
mutableString += " now!"
```



{% hint style="info" %}
<mark style="color:red;">**注意引号**</mark>

1、单引号：没有特殊用途

2、双英好：包括内容为字符串

3、三对双引号：声明多行字符串
{% endhint %}



####
