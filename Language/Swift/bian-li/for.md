---
description: 常见通过索引遍历的，都是针对有序的，数组和字符串
---

# for



{% hint style="info" %}
概览：

1、没有单独for

2、for..in

2、for...each
{% endhint %}

## 1、没有单独的for遍历

Q：为什么没有像C 语言那样的for的索引方式遍历呢？&#x20;

A: 因为在for...in 里面有更加简单的方式使用索引和对应的值了，所以这个单独的方式没有必要了。



## 2、for..in 遍历

### 2.1 遍历有序集合

#### 1）直接遍历值

```
let array = ["苹果", "香蕉", "橘子"]
for fruit in array {
    print(fruit)
}
```

#### 2）通过索引遍历值

```
let array = ["苹果", "香蕉", "橘子"]
for i in 0..<array.count {
    print("第 \(i) 个元素是 \(array[i])")
}
```

#### 3）同时获取<mark style="color:red;">索引和元素 ，</mark>使用 `enumerated()`&#x20;

```
let array = ["苹果", "香蕉", "橘子"]
for (index, fruit) in array.enumerated() {
    print("第 \(index) 个元素是 \(fruit)")
}
```

#### 4）范围遍历（Range)

使用 `for-in` 结合范围操作符来遍历数值区间。

```
for number in 1...5 {
    print(number)
}

# 如果不想包括上限，可以使用半开区间 ..<
for number in 1..<5 {
    print(number)
}
```

#### 5）步长遍历索引 stride(from:to:by:)

按一定步长遍历索引，从而访问特定索引位置的元素。

```
let array = ["A", "B", "C", "D", "E"]
for i in stride(from: 0, to: array.count, by: 2) {
    print("第 \(i) 个元素是 \(array[i])")
}
```

### 2.2便利无序集合

#### 1) 遍历字典（无序集合）

```
let fruits = ["苹果": 5, "香蕉": 3, "橘子": 8]
for (fruit, quantity) in fruits {
    print("\(fruit): \(quantity)个")
}
```

## 3、forEach方法

数组、字典等集合类型还支持 `forEach` 方法，允许你通过闭包遍历集合的每个元素。

```
let array = ["苹果", "香蕉", "橘子"]
array.forEach { fruit in
    print(fruit)
}
```



***

<mark style="color:red;">Q： 有了for.in 为什么还需要forEach?</mark>

A: `forEach` 语法更加简洁，尤其在**简单的遍历**操作中十分常用。

<mark style="color:red;">Q: 如果这样，那么单独的for也不应该去掉？</mark>

A：

1、for和for..in 是包含关系，并且for..in比for更加简洁， for..in 可以索引遍历，可以索引+值遍历。

2、for..in和forEach没有包含关系，for..in替代我们传统的for遍历，而forEach是更加适应了函数式链式编程，更加简洁的高阶函数。



## **for..in 和forEach在语法、用法** 各有不同：

### 1. **简洁性和函数式编程风格**

`forEach` 是 Swift 中函数式编程的一部分。

它使用闭包来处理集合中的每个元素，代码更简洁并且符合函数式编程的风格。

相比于 `for-in`，`forEach` 可以在一行代码中完成遍历，尤其适合简单的操作。

在某些场景下更符合现代编程的简洁需求，特别是在**处理链式操作**时。

```
let array = ["苹果", "香蕉", "橘子"]
array.forEach { print($0) }
```

### 2. **无返回值和不可提前退出**

`forEach` 不允许 `break` 或 `continue`，即你无法在中途停止循环。

for..in 适合中间有判断退出停止循环

forEach 不需要跳出的场景

```
// 这段代码会报错，因为 forEach 不允许 break
array.forEach { fruit in
    if fruit == "香蕉" {
        break // 错误：forEach 中不能使用 break
    }
}
```

```
for fruit in array {
    if fruit == "香蕉" {
        break // 可以中途退出
    }
}
```

### 3. **更适合链式调用**

`forEach` 常用于与其他函数式方法（如 `map`、`filter`）结合使用，使代码看起来更加流畅和易读。

```
let numbers = [1, 2, 3, 4]
numbers.filter { $0 % 2 == 0 }.forEach { print($0) }
```

### 4. **代码风格选择**

选择 `for-in` 或 `forEach` 很大程度上取决于个人偏好和代码风格。对于一些开发者来说，`for-in` 更加直观和可读，尤其是在处理复杂逻辑时。而 `forEach` 更适合需要简洁代码的场景。



{% hint style="info" %}
总结：



* **`for-in`**：适合需要控制流（如 `break`、`continue`）的场景，更传统，灵活性高。
* **`forEach`**：适合简洁的遍历操作，尤其是函数式编程风格和链式调用，不允许中途退出循环。
{% endhint %}
