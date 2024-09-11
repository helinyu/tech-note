---
description: 数据常见的操作：增删改查 ,
---

# 3、操作

增删改查：

查： 访问 （元素、子数组、索引）

删： 删除， 删除中间、第一个、最后一个，多个

改： 替换

增： 增加， 增加中间，第一个，最后一个，多个

## 1、访问

### 1.1、索引下标方式访问



### 1.2、访问最后/第一个元素

通过first/last访问

```
let firstFruit = fruits.first  // Optional("苹果")
let lastFruit = fruits.last    // Optional("橘子")
```

### 1.3、访问子数组

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

### 2.1 基本的修改元素【索引方式】&#x20;



### 2.2 修改多个元素

#### 2.2.1、 通过for循环

#### 2.2.2、使用下标并赋值【多个连续的元素】

```
var fruits = ["苹果", "香蕉", "橘子", "草莓"]
fruits[1...2] = ["蓝莓", "芒果"]  // 将第二、第三个元素替换
```



## 3、增加

### 3.1 增加中间【插入】

insert( xx at:) 插入单个元素

insert(contentsOf: at:) 插入子数组

```
var array = [10, 20, 20, 20 ,30 ,40]
array.insert(11, at: 1)
array.insert(contentsOf: [22, 22], at: 3)
array.forEach { a in
    print(a)
}
```

### 3.2 增加到末尾【添加】

append()

append(contentsOf:)

```
var array = [10, 20, 20, 20 ,30 ,40]
array.append(5) // 添加打个元素
array.append(contentsOf: [4,4])// 添加子数组
array.forEach { a in
    print(a)
}
```

## 4、删除

**4.1 删除元素**：使用 `remove(at:)` 方法可以删除指定索引的元素：

```
var fruits = ["苹果", "香蕉", "橘子"]
fruits.remove(at: 1)  // 删除第二个元素 "香蕉"
```

### 4.2 删除最后元素

removeLast()



## 5、count数目

* `count`：获取数组中的元素个数。

```
let numberOfFruits = fruits.count  // 数组元素个数
```



## 6、是否为空

* `isEmpty`：检查数组是否为空。

```
let isArrayEmpty = fruits.isEmpty  // 是否为空

```

## 7、 **安全访问数组元素**

为了避免数组越界访问，可以使用 `optional` 绑定的方式来安全地访问数组元素：

```
if let fruit = fruits[safe: 2] {
    print(fruit)
} else {
    print("索引无效")
}
可以避免因为越界访问而导致的崩溃
```

## 8、索引

### 8.1 、startIndex/endIndex第一个/最后一个索引

startIndex 对于数组来说永远都是0，&#x20;

endIndex 返回最后一个元素索引的位置+1，  对于数组来说== count

如果数组为空，startIndex == endIndex&#x20;

### 8.2、查找索引

firstIndex(of:)返回给**定的元素**在数组中出现的第一个位置(optional)

lastIndex(of:) 返回**给定的元素**在数组中出现的最后一个位置(optional)

firstIndex(where:)返回符合条件在数组中出现的第一个位置(optional)

lastIndex(where:) 返回复合条件在数组中出现的最后一个位置(optional)

```
var array = [10, 20, 20, 20 ,30 ,40]
print(array.lastIndex(of: 20))
print(array.firstIndex(of: 20))
print(array.firstIndex(where: {$0 > 20}))
print(array.firstIndex(where: {$0 > 20}))
```

## 9、获取索引区间 indices

```
let array = ["A", "B", "C", "D", "E"]
for index in array.indices {
    print(index)
}
```

获取数组索引的方式：

### 1、通过索引区间indices

### 2、通过`enumerated()`

### 3、通过count获取数量变量



## 10、判断是否包含指定元素

contains(\_:) 判断数组是否包含指定元素

contains(where:) 判断数组是否包含符合条件的元素



## 11、判断所有元素符合某个条件

allSatisfy(\_:) 判断数组的每个元素都符合给定的条件

```
var array = [10, 20 ,30 ,40]
print(array.allSatisfy({$0 > 4})) // true
print(array.allSatisfy({$0 > 10})) //false
```

## 12、最大、小元素

max() 最大元素

min() 最小元素

max(by:) 利用给定的方式比较并返回数组中最大的元素

min(by:) 利用给定的方式比较并返回数组中最小的元素

```
var array = [10, 20, 20, 20 ,30 ,40]
print(array.max())
print(array.min())
```

```
let array = [(45, "error1"), (30, "error2"), (50, "error3")]
print(array.min{a, b in a.0 < b.0})
print(array.max{a, b in a.0 < b.0})
输出：
Optional((30, "error2"))
Optional((50, "error3"))
```

## 小结

{% hint style="info" %}
* **查/访问**
  * 元素：使用**索引访问**元素。便利方式：first、last访问第一个和最后一个
  * 子数组：通过**索引范围**访问子数组。
* **修改**：
  * 元素：使用**索引修改**可变数组的元素。【元素的长度不会变】
  * 子数组：
* **增加**：&#x20;
  * **添加:**&#x20;
    * 元素 append()
    * 子数组 append(contentsOf:)
  * **`插入:`**
    * `元素 insert(xx, at:)`
    * `子数组：insert`(contentsOf: at:)
* **删除**：&#x20;
  * 元素：和 `remove(at:)` 方法。
  * 子数组
* **索引**&#x20;
  * **startIndex  / of /where**
  * **endIndex / of /where**&#x20;
{% endhint %}

