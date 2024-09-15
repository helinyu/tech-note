# 闭包

在 Python 中，闭包（Closure）是一种特殊的函数。它是由一个函数和与其相关的引用环境组合而成的实体。

**一、闭包的构成**

1. 外部函数（enclosing function）：包含内部函数的函数。
2. 内部函数（inner function）：定义在外部函数内部的函数。
3. 引用环境：外部函数中被内部函数引用的变量。

**二、闭包的特点**

1. 内部函数可以访问外部函数的变量：即使外部函数已经执行完毕，内部函数仍然可以访问外部函数中的变量。这是因为内部函数保留了对外部函数变量的引用。
2. 闭包可以记住外部函数的变量值：每次调用外部函数时，都会创建一个新的闭包，内部函数可以记住外部函数在创建闭包时的变量值。
3. 闭包可以作为返回值：外部函数可以返回内部函数，从而创建一个闭包。这个闭包可以在外部函数执行完毕后继续存在，并可以被其他代码调用。

**三、闭包的示例**

以下是一个简单的闭包示例：

```python
def outer_function(x):
    def inner_function(y):
        return x + y
    return inner_function

closure = outer_function(10)
print(closure(5))  
# 输出：15
```

在这个示例中，`outer_function` 是外部函数，它接受一个参数 `x`，并返回一个内部函数 `inner_function`。内部函数 `inner_function` 接受一个参数 `y`，并返回 `x + y` 的结果。

当调用 `outer_function(10)` 时，它返回一个闭包，这个闭包记住了外部函数中的变量 `x` 的值为 10。然后，将这个闭包赋值给变量 `closure`。当调用 `closure(5)` 时，内部函数 `inner_function` 使用记住的 `x` 的值 10 和传入的参数 `y` 的值 5，计算并返回结果 15。

**四、闭包的应用场景**

1. 数据隐藏和封装：闭包可以用于隐藏外部函数中的变量，只暴露必要的接口给外部代码。这有助于实现数据封装和信息隐藏。
2. 函数工厂：闭包可以用于创建函数工厂，即根据不同的参数生成不同的函数。
3. 装饰器：闭包是实现装饰器的基础。装饰器是一种用于修改现有函数行为的函数，它通常使用闭包来保存被装饰函数的状态。

总之，闭包是 Python 中一个强大的特性，它允许函数记住其外部环境的状态，并提供了一种灵活的方式来实现数据隐藏、函数工厂和装饰器等功能。