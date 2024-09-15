# 函数

Python 中的函数是将一段可复用的代码封装起来的机制，通过调用函数可以多次执行相同的操作。Python 提供了灵活的函数定义方式，可以带有参数、返回值、默认参数等，还可以是匿名函数（`lambda` 表达式）。

## 1. **函数的定义和调用**

在 Python 中，使用 `def` 关键字定义一个函数，函数名遵循命名规范（通常使用小写字母和下划线），函数可以接受参数，并返回值。

**语法：**

```python
def function_name(parameters):
    # 函数体
    return value
```

* **`function_name`**：函数名。
* **`parameters`**：可选的参数列表，参数之间用逗号分隔。
* **`return`**：返回值（可选），如果不写 `return`，函数会返回 `None`。

**示例：简单的函数定义与调用**

```python
def greet(name):
    return f"Hello, {name}!"

message = greet("Alice")
print(message)  # 输出：Hello, Alice!
```

## 2. **参数**

函数可以接受参数，也可以设置默认值。参数有多种类型，如位置参数、关键字参数、可变参数等。

### **(1) 位置参数**

这是最常见的参数传递方式，按照参数顺序进行传递。

```python
def add(a, b):
    return a + b

print(add(3, 5))  # 输出：8
```

### **(2) 关键字参数**

可以在调用时明确指定参数的名字，使得顺序不重要。

```python
def introduce(name, age):
    return f"My name is {name} and I am {age} years old."

print(introduce(age=30, name="Bob"))  # 输出：My name is Bob and I am 30 years old.
```

### **(3) 默认参数**

在函数定义时可以为参数设置默认值，调用时如果不传入对应的参数，则使用默认值。

```python
def greet(name="Guest"):
    return f"Hello, {name}!"

print(greet())         # 输出：Hello, Guest!
print(greet("Alice"))  # 输出：Hello, Alice!
```

### **(4) 可变参数**

* **`*args`**：用于接受不定数量的位置参数，函数内部将其作为元组处理。
* **`**kwargs`**：用于接受不定数量的关键字参数，函数内部将其作为字典处理。

```python
# 使用 *args
def sum_all(*args):
    return sum(args)

print(sum_all(1, 2, 3, 4))  # 输出：10

# 使用 **kwargs
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="New York")
# 输出：
# name: Alice
# age: 25
# city: New York
```

## 3. **返回值**

使用 `return` 语句可以从函数返回一个值，若没有 `return`，函数默认返回 `None`。一个函数也可以返回多个值。

**示例：返回单个值**

```python
def square(x):
    return x * x

print(square(5))  # 输出：25
```

**示例：返回多个值**

```python
def get_person():
    name = "Alice"
    age = 30
    return name, age

person_name, person_age = get_person()
print(person_name)  # 输出：Alice
print(person_age)   # 输出：30
```

## 4. **作用域**

* **局部变量**：在函数内部定义的变量，其作用域仅限于函数内部。
* **全局变量**：在函数外部定义的变量，可以在整个模块中访问。

```python
x = 10  # 全局变量

def modify():
    x = 5  # 局部变量
    print("Inside function:", x)

modify()  # 输出：Inside function: 5
print("Outside function:", x)  # 输出：Outside function: 10
```

如果想在函数内部修改全局变量，需要使用 `global` 关键字。

```python
x = 10

def modify():
    global x
    x = 5

modify()
print(x)  # 输出：5
```

## 5. **匿名函数（Lambda 表达式）**

匿名函数使用 `lambda` 关键字定义，它是一个简短的函数，可以有任意数量的参数，但只能有一个表达式。

**语法：**

```python
lambda parameters: expression
```

**示例：简单的 `lambda` 函数**

```python
square = lambda x: x * x
print(square(5))  # 输出：25

add = lambda a, b: a + b
print(add(3, 5))  # 输出：8
```

**示例：`lambda` 和 `map()`、`filter()` 结合使用**

```python
numbers = [1, 2, 3, 4, 5]

# 使用 map 函数应用 lambda 表达式
squared = list(map(lambda x: x * x, numbers))
print(squared)  # 输出：[1, 4, 9, 16, 25]

# 使用 filter 函数应用 lambda 表达式
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # 输出：[2, 4]
```

## 6. **嵌套函数**

在 Python 中，可以在一个函数内部定义另一个函数，这样的函数称为嵌套函数。

```python
def outer_function():
    def inner_function():
        print("This is the inner function")
    inner_function()

outer_function()
# 输出：
# This is the inner function
```

## 7. **闭包（Closure）**

闭包是指函数内部的函数引用了外部函数的变量，并且在外部函数执行完毕后，这些引用仍然有效。

```python
def outer(x):
    def inner(y):
        return x + y
    return inner

add_five = outer(5)
print(add_five(3))  # 输出：8
```

## 8. **装饰器（Decorator）**

装饰器是一种特殊的函数，它可以在不修改原函数的情况下增强或改变其功能。装饰器通常使用 `@decorator_name` 语法。

```python
def decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@decorator
def say_hello():
    print("Hello!")

say_hello()
# 输出：
# Before function call
# Hello!
# After function call
```

## 9. **递归函数**

递归函数是指函数在其定义中调用自身，通常用于解决分而治之的问题，如计算阶乘、斐波那契数列等。

**示例：计算阶乘**

```python
def factorial(n):
    if n == 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 输出：120
```



## 10、**文档字符串（docstring）**

可以在函数定义的下一行使用三引号来添加文档字符串，描述函数的功能和参数。\
pythonCopy

```
def add(a, b):
    """
    This function adds two numbers.

    Args:
        a: The first number.
        b: The second number.

    Returns:
        The sum of a and b.
    """
    return a + b
```



## 总结：

* **定义函数** 使用 `def` 关键字。
* 函数可以带有**位置参数、关键字参数、默认参数和可变参数**。
* 函数可以**返回一个值或多个值**，使用 `return`。
* Python 允许**嵌套函数、匿名函数、递归函数以及闭包**。
* 使用装饰器可以在不修改原函数的情况下增强其功能。
* 文档字符串，特殊的注释吧了
