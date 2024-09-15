# 判断

## 1、 if..else if ...else&#x20;



## 2、复合条件

使用逻辑运算符（`&&`（与）、`||`（或）、`!`（非））组合多个条件。

```
   let num = 10
   if num > 5 && num < 15 {
       print("Number is between 5 and 15")
   }
```

## 3、guard 语句：

用于提前退出函数或方法，通常用于检查输入参数的有效性。

```swift
guard condition else {    // 如果条件不满足，提前退出函数或方法  
  return
}
```

## **4、在`switch`语句中的控制转移**：

* 除了使用`fallthrough`，还可以在`switch`语句中使用`break`来提前退出整个`switch`语句。
* 示例：
* 注意， 这里的switch执行复合之后就会跳出去，可以使用`fallthrough 让它继续执行。`

```swift
   let char = "a"
   switch char {
   case "a":
       print("It's 'a'")
       break
   default:
       print("Other character")
   }
```



## 5、**标签语句**：

* 在嵌套循环中，可以使用标签来标识特定的循环，以便在`break`或`continue`时指定要中断或跳过的循环。
* 示例：

```swift
   outerLoop: for i in 1...3 {
       for j in 1...3 {
           if j == 2 {
               break outerLoop
           }
           print("\(i), \(j)")
       }
   }
```

