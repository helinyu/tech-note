---
description: 数据常见的操作：增删改查
---

# 3、操作

## 1、访问

### 1.1、索引下标方式访问



### 1.2、访问最后/第一个元素

通过first/last访问

```
let firstFruit = fruits.first  // Optional("苹果")
let lastFruit = fruits.last    // Optional("橘子")
```

1.3、访问子数组

通过指定索引范围来访问数组的一个子集，使用下标语法来获取数组的子数组：

```
let fruits = ["苹果", "香蕉", "橘子", "草莓"]
let someFruits = fruits[1...2]  // 访问第二个和第三个元素 ["香蕉", "橘子"]
```

这里返回的子数组是 `ArraySlice` 类型，而不是标准的 `Array`。如果需要标准数组，可以将其转换为数组：

```
let someFruitsArray = Array(fruits[1...2])
```

## 2、修改【替换】

2.1 基本的修改元素【索引方式】&#x20;



2.2 修改多个元素

2.2.1、 通过for循环

2.2.2、使用下标并赋值【多个连续的元素】

```
var fruits = ["苹果", "香蕉", "橘子", "草莓"]
fruits[1...2] = ["蓝莓", "芒果"]  // 将第二、第三个元素替换
```
