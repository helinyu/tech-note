# 控制语句

在Scala中，控制语句用于控制程序的执行流。以下是一些常见的控制语句：

1. **条件语句**：
   *   `if` 语句：

       ```scala
       val x = 10
       if (x > 0) {
         println("x is positive")
       } else {
         println("x is non-positive")
       }
       ```
   *   `if` 表达式（可以返回值）：

       ```scala
       val result = if (x > 0) "positive" else "non-positive"
       ```
   *   `match` 语句（类似于 switch）：

       ```scala
       val x = 2
       x match {
         case 1 => println("one")
         case 2 => println("two")
         case _ => println("other")
       }
       ```
2. **循环语句**：
   *   `for` 循环：

       ```scala
       for (i <- 1 to 5) {
         println(i)
       }
       ```
   *   `while` 循环：

       ```scala
       var i = 5
       while (i > 0) {
         println(i)
         i -= 1
       }
       ```
   *   `do-while` 循环：

       ```scala
       var i = 5
       do {
         println(i)
         i -= 1
       } while (i > 0)
       ```
3. **控制抽象**：
   *   <mark style="color:red;">`break`</mark> <mark style="color:red;"></mark><mark style="color:red;">和</mark> <mark style="color:red;"></mark><mark style="color:red;">`continue`</mark> <mark style="color:red;"></mark><mark style="color:red;">在Scala中不是直接支持的，但可以使用</mark>`scala.util.control.Breaks`：

       ```scala
       import scala.util.control.Breaks._

       breakable {
         for (i <- 1 to 10) {
           if (i == 5) break() // 退出循环
           println(i)
         }
       }
       ```

