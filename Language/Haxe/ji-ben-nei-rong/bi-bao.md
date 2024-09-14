# 闭包

Lambda 这个其实就是一个匿名函数—— 闭包



在 Haxe 中，可以使用 lambda 表达式（也称为匿名函数）来创建简短的函数。

以下是一个使用 lambda 表达式的示例：

```haxe
var numbers = [1, 2, 3, 4, 5];

// 使用 lambda 表达式过滤出大于 2 的数字
var filteredNumbers = numbers.filter(function(item) {
    return item > 2;
});

trace(filteredNumbers);
```

在这个例子中，`filter`方法接受一个函数作为参数，这个函数就是一个 lambda 表达式。它检查每个元素是否大于 2，并返回一个布尔值。

Lambda 表达式也可以作为参数传递给其他函数，或者赋值给变量：

```haxe
var add = function(a, b) {
    return a + b;
};

trace(add(3, 4)); // 7
```

Lambda 表达式还可以使用参数类型注解和返回类型注解：

```haxe
var multiply = function(a:Int, b:Int):Int {
    return a * b;
};

trace(multiply(2, 3)); // 6
```

Haxe 的 lambda 表达式可以非常方便地进行函数式编程，使代码更加简洁和可读。
