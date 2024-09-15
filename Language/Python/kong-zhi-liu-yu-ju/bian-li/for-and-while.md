# for & while

在 Python 中，循环遍历是对可迭代对象（如列表、元组、字符串、字典等）中的元素逐一进行操作的方式。主要有两种循环结构可以实现遍历：**`for` 循环** 和 **`while` 循环**。



> Python 的 `for` 语句不迭代算术递增数值（如 Pascal），或是给予用户定义迭代步骤和结束条件的能力（如 C），而是在列表或字符串等任意序列的元素上迭代，按它们在序列中出现的顺序。 即为和C不一样，没有i++这玩意



> 没有do ..while ,没有forEach ，没有for..of ，
>
> 只有for.in , while&#x20;

## 1. **`for` 循环**

`for` 循环是一种用于遍历可迭代对象的循环结构，语法非常简单。它会自动获取可迭代对象中的每一个元素。&#x20;

**语法：**

```python
for element in iterable:
    # 对 element 执行某些操作
```

**示例：遍历列表**

```python
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)
# 输出：
# 1
# 2
# 3
# 4
# 5
```

**示例：遍历字符串**

```python
s = "Python"
for char in s:
    print(char)
# 输出：
# P
# y
# t
# h
# o
# n
```

## 2. **`while` 循环**

`while` 循环根据条件表达式的真假来控制循环的执行，它在不确定循环次数的情况下非常有用。通常需要使用一个计数器或索引来手动控制遍历。

**语法：**

```python
while condition:
    # 执行操作
```

**示例：用 `while` 循环遍历列表**

```python
numbers = [1, 2, 3, 4, 5]
i = 0
while i < len(numbers):
    print(numbers[i])
    i += 1
# 输出：
# 1
# 2
# 3
# 4
# 5
```

## 3. **常用的遍历模式**

### **(1) 使用 `range()` 函数**

`range()` 用于生成一个数值序列，常与 `for` 循环配合使用。它常用于按索引遍历可迭代对象。

```python
for i in range(5):
    print(i)
# 输出：
# 0
# 1
# 2
# 3
# 4
```

### **(2) 带索引的遍历：使用 `enumerate()`**

`enumerate()` 函数可以在遍历时同时获取元素的索引和元素本身，非常适合在需要索引的情况下使用。

```python
fruits = ['apple', 'banana', 'cherry']
for index, fruit in enumerate(fruits):
    print(f"Index: {index}, Fruit: {fruit}")
# 输出：
# Index: 0, Fruit: apple
# Index: 1, Fruit: banana
# Index: 2, Fruit: cherry
```

### **(3) 遍历字典：使用 `items()`**

字典可以通过 `items()` 方法同时遍历键和值。

```python
d = {'a': 1, 'b': 2, 'c': 3}
for key, value in d.items():
    print(f"Key: {key}, Value: {value}")
# 输出：
# Key: a, Value: 1
# Key: b, Value: 2
# Key: c, Value: 3
```

### **(4) 遍历多个列表：使用 `zip()`**

`zip()` 函数可以将多个可迭代对象并行遍历。

```python
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 35]
for name, age in zip(names, ages):
    print(f"{name} is {age} years old")
# 输出：
# Alice is 25 years old
# Bob is 30 years old
# Charlie is 35 years old
```

## 4. **控制循环的关键字**

### **(1) `break`**

`break` 用于立即终止整个循环，循环体中的剩余语句将不会执行。

```python
for i in range(10):
    if i == 5:
        break
    print(i)
# 输出：
# 0
# 1
# 2
# 3
# 4
```

### **(2) `continue`**

`continue` 用于跳过当前迭代中的剩余语句，继续下一次迭代。

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
# 输出：
# 0
# 1
# 3
# 4
```

### **(3) `else` 与循环**

循环中的 `else` 子句在循环正常结束（即没有被 `break` 打断）时执行。

```python
for i in range(5):
    print(i)
else:
    print("Loop ended naturally")
# 输出：
# 0
# 1
# 2
# 3
# 4
# Loop ended naturally
```

如果循环被 `break` 终止，`else` 部分不会执行。

## 5. **嵌套循环**

在 Python 中，可以将一个循环放在另一个循环内，这称为嵌套循环。常用于处理二维数据结构（如二维列表）。

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
for row in matrix:
    for item in row:
        print(item, end=' ')
    print()  # 换行
# 输出：
# 1 2 3 
# 4 5 6 
# 7 8 9
```

## 6. **遍历生成器和迭代器**

生成器和迭代器也是可迭代对象，通常用于处理大量数据或无限序列。可以通过 `for` 循环直接遍历生成器。

**示例：遍历生成器**

```python
def my_generator():
    yield 1
    yield 2
    yield 3

for value in my_generator():
    print(value)
# 输出：
# 1
# 2
# 3
```

## 7. **`while` 循环与条件控制**

当你需要根据某个条件循环，直到条件变为 `False` 时，`while` 循环是最佳选择。例如，当处理某些计算问题，或者等待某个状态改变时：

```python
count = 0
while count < 5:
    print(count)
    count += 1
# 输出：
# 0
# 1
# 2
# 3
# 4
```

## 总结：

* **`for` 循环**：适用于遍历所有可迭代对象，是最常用的循环结构。
* **`while` 循环**：适用于基于条件控制的循环，特别是当循环次数不确定时。
* 通过 `enumerate()`、`zip()` 等辅助函数，可以方便地实现带索引或多对象的并行遍历。
* `break` 和 `continue` 用于控制循环的执行，`else` 语句与循环结合可以在特殊场景下使用。



## 小结：

1、for 循环， 常见for.. 加一个关键字使用

2、while 常见的循环，具有循环遍历和条件控制的能力

3、break 和continue 是否有，和C常规一样，还多了else ， 正常退出循环的时候执行

4、（索引、索引+值、值）范围遍历、索引遍历、遍历数组、字典、集合

5、zip方式支持了多个遍历

