# 函数注释

在 Python 中，函数注释（也称为文档字符串或 **docstring**）是用于描述函数的功能、参数、返回值及其他相关信息的文本。函数注释通常用于提高代码的可读性和可维护性，并且工具如 `help()` 可以自动提取这些注释。Python 中的函数注释主要通过三引号字符串（`"""` 或 `'''`）进行编写。

## 1. **基本函数注释格式**

通常，在函数定义的第一行使用三引号（单引号或双引号均可），写入函数的用途说明、参数和返回值。如下是一个基本的例子：

```python
def add(x, y):
    """
    计算两个数的和。

    参数:
    x (int or float): 第一个数字。
    y (int or float): 第二个数字。

    返回:
    int or float: 两个数字的和。
    """
    return x + y
```

## 2. **文档字符串的位置**

* 文档字符串必须放置在函数定义下的第一行，在函数体之前。
* 函数的文档字符串通常简明扼要描述该函数的作用，特别是在大型项目中，文档字符串能显著提高代码的可读性。

## 3. **查看函数注释**

可以使用 Python 内置的 `help()` 函数或者通过 `.__doc__` 属性来查看文档字符串。

```python
print(add.__doc__)
```

输出：

```
计算两个数的和。

参数:
x (int or float): 第一个数字。
y (int or float): 第二个数字。

返回:
int or float: 两个数字的和。
```

## 4. **注释规范**

虽然 Python 对函数注释的格式没有强制规定，但通常推荐遵循一些社区约定的文档格式规范，如：

* **Google 风格**：简单且结构清晰，广泛使用。
* **NumPy 风格**：科学计算库 `NumPy` 所采用的风格，适用于技术文档较多的场合。
* **reStructuredText (reST)**：适用于 `Sphinx` 等文档生成工具的标准格式。

**Google 风格的注释**

```python
def add(x, y):
    """
    计算两个数的和。

    Args:
        x (int or float): 第一个数字。
        y (int or float): 第二个数字。

    Returns:
        int or float: 两个数字的和。
    """
    return x + y
```

**NumPy 风格的注释**

```python
def add(x, y):
    """
    计算两个数的和。

    Parameters
    ----------
    x : int or float
        第一个数字。
    y : int or float
        第二个数字。

    Returns
    -------
    int or float
        两个数字的和。
    """
    return x + y
```

**reStructuredText (reST) 风格的注释**

```python
def add(x, y):
    """
    计算两个数的和。

    :param x: 第一个数字。
    :type x: int or float
    :param y: 第二个数字。
    :type y: int or float
    :return: 两个数字的和。
    :rtype: int or float
    """
    return x + y
```

## 5. **函数类型注解**

Python 还支持 **类型注解** 来描述函数参数和返回值的类型。类型注解不会影响代码的运行，但可以提高代码的可读性和便于静态类型检查工具（如 `mypy`）的使用。

**语法：**

```python
def add(x: int, y: int) -> int:
    """
    计算两个整数的和。

    参数:
    x (int): 第一个整数。
    y (int): 第二个整数。

    返回:
    int: 两个整数的和。
    """
    return x + y
```

* `x: int` 和 `y: int` 表示参数 `x` 和 `y` 应该是整数类型。
* `-> int` 表示该函数返回的结果应为整数类型。

## 6、 `__annotations__ ：`函数的注释信息可以通过特殊属性 `__annotations__` 来访问。

以下是一个示例：

```python
def add_numbers(a: int, b: int) -> int:
    return a + b

print(add_numbers.__annotations__)
```

输出：

```
{'a': <class 'int'>, 'b': <class 'int'>, 'return': <class 'int'>}
```

`__annotations__` 返回一个字典，其中键是参数名（包括 `return` 表示返回值），值是对应的注释内容。

这个特性可以用于在运行时获取函数的注释信息，也可以被一些框架和工具用来进行更高级的代码分析和处理。但要注意，这些注释只是提供信息，Python 并不会强制按照注释进行类型检查等操作。

## **总结**

* **文档字符串（docstring）** 是对函数、类、模块等的描述，能提高代码的可读性和可维护性。
* 函数注释通常包括函数功能、参数、返回值等信息。
* 不同的文档风格（Google、NumPy、reST）适合不同的项目需求。
* **类型注解** 可以进一步明确函数参数和返回值的类型，提高代码质量。

文档字符串和类型注解的结合有助于编写更加健壮、易于理解和维护的 Python 代码。
