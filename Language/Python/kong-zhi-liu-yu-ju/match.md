# match

> 接受一个表达式并把它的值与一个或多个 case 块给出的一系列模式进行比较。
>
> 这表面上像 C、Java 或 JavaScript（以及许多其他程序设计语言）中的 switch 语句，但其实它更像 Rust 或 Haskell 中的模式匹配。
>
> 只有第一个匹配的模式会被执行，并且它还可以提取值的组成部分（序列的元素或对象的属性）赋给变量。



在 Python 3.10 中引入了一个新特性，叫做 **`match` 语句**，它是 **结构化模式匹配**（Structural Pattern Matching）的实现。`match` 类似于其他编程语言中的 `switch-case` 语句，但功能更加灵活和强大。它允许我们根据对象的结构和类型来进行模式匹配，适用于各种复杂的条件分支判断。

#### 1. **`match` 语句的基本语法**

**语法结构：**

```python
match value:
    case pattern1:
        # 当匹配 pattern1 时执行
    case pattern2:
        # 当匹配 pattern2 时执行
    case _:
        # 默认情况，相当于 switch-case 中的 default
```

* **`match value`**：`value` 是要进行匹配的表达式或变量。
* **`case pattern`**：`pattern` 是我们希望匹配的结构或值，如果匹配成功，执行相应的代码块。
* **`_`**：下划线是通配符，表示匹配任何值，相当于默认情况。

#### 2. **`match` 语句的简单示例**

**示例1：匹配具体值**

```python
def http_error(status):
    match status:
        case 400:
            return "Bad Request"
        case 404:
            return "Not Found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"

print(http_error(404))  # 输出：Not Found
```

在这个例子中，`status` 的值将根据不同的 `case` 进行匹配，如果没有匹配到具体值，则进入默认的 `case _`。

#### 3. **使用通配符模式**

通配符模式 `_` 可以匹配任何值，通常用作最后的 `case`，处理未匹配到的情况。

**示例：使用 `_` 作为默认情况**

```python
def process_number(x):
    match x:
        case 1:
            print("One")
        case 2:
            print("Two")
        case _:
            print("Something else")

process_number(1)  # 输出：One
process_number(3)  # 输出：Something else
```

#### 4. **解构和模式匹配**

`match` 语句不仅可以匹配简单的值，还可以匹配数据结构（如元组、列表、字典等）的内部结构。

**示例：匹配元组**

```python
def point_info(point):
    match point:
        case (0, 0):
            return "Origin"
        case (0, y):
            return f"Y-axis at {y}"
        case (x, 0):
            return f"X-axis at {x}"
        case (x, y):
            return f"Point at ({x}, {y})"

print(point_info((0, 0)))    # 输出：Origin
print(point_info((0, 5)))    # 输出：Y-axis at 5
print(point_info((3, 0)))    # 输出：X-axis at 3
print(point_info((2, 3)))    # 输出：Point at (2, 3)
```

在这个例子中，`match` 能够匹配元组的结构，并通过变量 `x` 和 `y` 捕获对应的值。

#### 5. **匹配列表**

除了元组外，`match` 也可以匹配列表等序列类型。

**示例：匹配列表**

```python
def process_list(lst):
    match lst:
        case []:
            return "Empty list"
        case [x]:
            return f"Single element: {x}"
        case [x, y]:
            return f"Two elements: {x} and {y}"
        case [x, y, *rest]:
            return f"First two: {x}, {y}, and the rest: {rest}"

print(process_list([]))             # 输出：Empty list
print(process_list([1]))            # 输出：Single element: 1
print(process_list([1, 2]))         # 输出：Two elements: 1 and 2
print(process_list([1, 2, 3, 4]))   # 输出：First two: 1, 2, and the rest: [3, 4]
```

在这个例子中，`[x, y, *rest]` 是一个列表解构的模式，它会匹配至少有两个元素的列表，并将剩余部分赋给 `rest`。

#### 6. **匹配字典**

同样地，`match` 也可以匹配字典。

**示例：匹配字典**

```python
def process_dict(d):
    match d:
        case {"name": name, "age": age}:
            return f"Name: {name}, Age: {age}"
        case {"name": name}:
            return f"Name: {name}"
        case _:
            return "Unknown structure"

print(process_dict({"name": "Alice", "age": 30}))  # 输出：Name: Alice, Age: 30
print(process_dict({"name": "Bob"}))               # 输出：Name: Bob
print(process_dict({"age": 25}))                   # 输出：Unknown structure
```

这里的 `{"name": name, "age": age}` 是字典的结构匹配模式，允许我们直接解构字典中的值。

#### 7. **守卫（Guard）模式**

你可以为每个 `case` 添加守卫条件，即在匹配模式的基础上加上额外的判断条件。

**示例：带守卫条件的模式匹配**

```python
def process_number(x):
    match x:
        case x if x > 0:
            return "Positive"
        case x if x < 0:
            return "Negative"
        case 0:
            return "Zero"

print(process_number(10))  # 输出：Positive
print(process_number(-5))  # 输出：Negative
print(process_number(0))   # 输出：Zero
```

在这个例子中，`if x > 0` 和 `if x < 0` 是守卫条件，用于在模式匹配成功的基础上进一步限制匹配条件。

#### 8. **对象模式匹配**

`match` 语句可以与类对象结合，匹配对象的属性。

**示例：匹配类对象**

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

def process_point(p):
    match p:
        case Point(x=0, y=0):
            return "Origin"
        case Point(x, y):
            return f"Point at ({x}, {y})"

p1 = Point(0, 0)
p2 = Point(1, 2)

print(process_point(p1))  # 输出：Origin
print(process_point(p2))  # 输出：Point at (1, 2)
```

在这个例子中，`Point(x=0, y=0)` 匹配具有特定属性值的 `Point` 对象，`Point(x, y)` 则匹配任何 `Point` 对象并解构其属性。

## 总结：

* Python 的 `match` 语句是结构化模式匹配的一部分，能够根据数据的结构和类型进行灵活的模式匹配。
* 它比传统的 `if-elif-else` 语句更直观，尤其适用于处理复杂的数据结构，如元组、列表、字典和对象。
* `match` 还支持守卫模式，可以结合条件判断来实现更灵活的匹配。

通过 `match`，可以使代码更加简洁易读，尤其适合处理复杂的分支逻辑和数据解构。



## 小结：

1、switch..case 这种C语言的方式将会被废弃掉，更多语言选择match这种，灵活的匹配模式。因为匹配的数据结构变得更加丰富

2.比if..elif..else更加之光，因为可以遍历元祖序列、列表、字典、集合、对象等等&#x20;

3.支持守卫模式，条件判断更加灵活

