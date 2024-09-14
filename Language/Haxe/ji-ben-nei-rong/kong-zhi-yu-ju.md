# 控制语句

在 Haxe 中，常见的控制语句有以下几种：

**一、条件判断语句**

1.  `if`-`else`语句：

    ```haxe
    var num = 10;
    if (num > 5) {
        trace("Number is greater than 5");
    } else {
        trace("Number is not greater than 5");
    }
    ```
2.  `switch`语句：

    ```haxe
    var day = "Monday";
    switch (day) {
        case "Monday":
            trace("It's Monday");
            break;
        case "Tuesday":
            trace("It's Tuesday");
            break;
        default:
            trace("Some other day");
    }
    ```

**二、循环语句**

1.  `for`循环：

    * 遍历一个范围：

    ```haxe
    for (i in 0...5) {
        trace(i);
    }
    ```

    * 遍历一个数组：

    ```haxe
    var arr = [1, 2, 3];
    for (item in arr) {
        trace(item);
    }
    ```
2.  `while`循环：

    ```haxe
    var count = 0;
    while (count < 5) {
        trace(count);
        count++;
    }
    ```
3.  `do`-`while`循环：

    ```haxe
    var num = 0;
    do {
        trace(num);
        num++;
    } while (num < 5);
    ```

**三、跳转语句**

1.  `break`：用于跳出循环或 `switch` 语句。

    ```haxe
    for (i in 0...10) {
        if (i == 5) {
            break;
        }
        trace(i);
    }
    ```
2.  `continue`：用于跳过当前循环迭代，继续下一次迭代。

    ```haxe
    for (i in 0...10) {
        if (i % 2 == 0) {
            continue;
        }
        trace(i);
    }
    ```

其实这个就是和C是一样的if、switch、for的使用。

