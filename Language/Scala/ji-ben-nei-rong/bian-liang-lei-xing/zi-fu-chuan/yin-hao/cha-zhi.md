# 插值

Scala支持三种主要的字符串插值方式：`s`、`f`和`raw`。

#### 1. `s` 插值

使用`s`前缀，你可以在字符串中直接插入变量和表达式。

```scala
val name = "Alice"
val age = 25
val greeting = s"Hello, my name is $name and I am $age years old."
println(greeting) // 输出: Hello, my name is Alice and I am 25 years old.
```

如果要插入复杂表达式，可以使用大括号：

```scala
val x = 10
val y = 5
println(s"The sum of $x and $y is ${x + y}.") // 输出: The sum of 10 and 5 is 15.
```

#### 2. `f` 插值

使用`f`前缀，你可以在字符串中使用格式化语法，与`printf`类似。

```scala
val price = 12.99
println(f"The price is $$price%.2f.") // 输出: The price is $12.99.
```

#### 3. `raw` 插值

使用`raw`前缀，字符串中的转义字符不会被处理，这对于需要输出原始字符串时非常有用。

```scala
val rawString = raw"This is a newline character: \n"
println(rawString) // 输出: This is a newline character: \n
```

#### 总结

字符串插值使得在字符串中嵌入变量和表达式变得简单且可读。你可以根据需要选择不同的插值方式来格式化字符串。如果你对字符串插值有更具体的问题或想了解更多示例，随时告诉我！
