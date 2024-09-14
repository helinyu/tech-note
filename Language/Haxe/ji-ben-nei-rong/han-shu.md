# 函数

在 Haxe 中，函数是一种重要的编程构造，可以接受输入参数并返回一个结果。

**一、函数的定义**

1. 基本语法：

```haxe
function add(a:Int, b:Int):Int {
    return a + b;
}
```

这里定义了一个名为 `add` 的函数，它接受两个整数参数 `a` 和 `b`，并返回它们的和，返回类型为整数。

2. 可选参数：

可以为函数定义可选参数，使用默认值。

```haxe
function greet(name:String, greeting:String = "Hello"):String {
    return greeting + ", " + name + "!";
}
```

在这个例子中，`greeting` 参数是可选的，默认值为 `"Hello"`。

**二、函数的调用**

1. 直接调用：

```haxe
var result = add(3, 5);
trace(result); // 输出 8
```

2. 使用可选参数：

```haxe
trace(greet("John")); // 输出 "Hello, John!"
trace(greet("Mary", "Hi")); // 输出 "Hi, Mary!"
```

**三、匿名函数和闭包**

1. 匿名函数：

可以创建匿名函数，即没有名称的函数。

```haxe
var multiply = function(a:Int, b:Int):Int {
    return a * b;
};
trace(multiply(4, 6)); // 输出 24
```

2. 闭包：

函数可以访问其外部作用域中的变量，形成闭包。

```haxe
var x = 10;
var closureFunc = function():Int {
    return x * 2;
};
trace(closureFunc()); // 输出 20
```

**四、函数作为参数和返回值**

1. 函数作为参数：

可以将函数作为参数传递给其他函数。

```haxe
function applyOperation(a:Int, b:Int, operation:Function):Int {
    return operation(a, b);
}
trace(applyOperation(3, 4, add)); // 输出 7
trace(applyOperation(5, 6, multiply)); // 输出 30
```

2. 函数作为返回值：

函数也可以返回另一个函数。

```haxe
function createAdder(num:Int):Function {
    return function(otherNum:Int):Int {
        return num + otherNum;
    };
}
var addFive = createAdder(5);
trace(addFive(3)); // 输出 8
```

Haxe 中的函数提供了强大的编程能力，可以灵活地组合和使用，以实现各种功能。



Haxe的函数，其实就是TS的函数类型模式。&#x20;

