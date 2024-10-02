# 基本内容

在Scala中，闭包是一个函数，其引用了其外部作用域中的变量。闭包可以捕获并“记住”其创建时的上下文，因此即使在外部作用域中变量的值发生变化，闭包依然可以访问当时的值。这使得闭包在处理状态和构建灵活的函数时非常有用。

#### 闭包的示例

1.  **基本闭包**：

    ```scala
    def makeCounter(): () => Int = {
      var count = 0
      () => {
        count += 1
        count
      }
    }

    val counter = makeCounter()
    println(counter()) // 输出: 1
    println(counter()) // 输出: 2
    println(counter()) // 输出: 3
    ```
2.  **捕获外部变量**：

    ```scala
    val multiplier = 3
    val multiply = (x: Int) => x * multiplier // multiplier被捕获
    println(multiply(5)) // 输出: 15
    ```
3.  **闭包与状态**： 闭包可以用于保存状态，这在实现状态机或计数器时非常有用。

    ```scala
    def createAccumulator(): (Int => Int) = {
      var total = 0
      (x: Int) => {
        total += x
        total
      }
    }

    val accumulator = createAccumulator()
    println(accumulator(10)) // 输出: 10
    println(accumulator(20)) // 输出: 30
    ```

#### 总结

闭包允许你在函数内部访问并修改外部变量的值，使得它们在编写更复杂的函数和维护状态时非常强大。如果你对闭包有更具体的问题或想要了解更多示例，随时告诉我！
