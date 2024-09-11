# while

`while 循环用于在满足特定条件时反复执行一段代码`



## 1、while

`while` 循环会首先检查条件，

如果条件为 `true`，则进入循环执行代码。

如果条件为 `false`，则跳出循环。

```
while 条件 {
    // 循环体
}

var number = 5
while number > 0 {
    print(number)
    number -= 1
}
//当 number 减到 0 时退出循环。
```



## 2、repeat..while

它会**先执行一次代码**，然后再检查条件。因此，即使条件一开始为 `false`，循环体也会至少执行一次。

```
repeat {
    // 循环体
} while 条件

var number = 0
repeat {
    print("number 是 \(number)")
    number += 1
} while number < 5
//repeat-while 循环会输出从 0 到 4 的数字，即使 number 初始值是 0，仍然会先执行一次循环。
```

## 3、迭代器+while

```
let array = ["A", "B", "C", "D", "E"]
var arrInterator = array.makeIterator()
while let ele = arrInterator.next() {
    print(ele)
}
```

迭代器的next判断，主要用于无序集合

## 4. **区别于 `for` 循环**

* **`while` 循环**：更适合那些**循环次数不确定**的场景，只要满足条件就会一直执行。
* **`for` 循环**：更适合那些**已知要执行固定次数**的场景（如遍历数组或范围）。

## 5. **注意事项**

* 如果 `while` 循环的条件一直为 `true`，而循环体中没有改变条件的逻辑，可能会导致**无限循环**。

```
while true {
    // 这是一个无限循环，必须通过 break 退出
    break
}
```



{% hint style="info" %}
### 总结

* **`while` 循环** 在执行前检查条件，适用于在条件为 `true` 时执行代码块。
* **`repeat-while` 循环** 先执行代码块，再检查条件，**保证循环体至少执行一次**。
{% endhint %}
