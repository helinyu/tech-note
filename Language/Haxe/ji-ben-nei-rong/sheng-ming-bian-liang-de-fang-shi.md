# 声明变量的方式

在 Haxe 中，可以使用以下方式声明变量：

1.  明确类型声明：

    ```haxe
    var myInt:Int = 10;
    var myString:String = "Hello";
    var myBool:Bool = true;
    ```
2.  类型推断：

    * 如果不明确指定类型，Haxe 编译器可以根据初始值进行类型推断。

    ```haxe
    var inferredVariable = 42; // 编译器推断为 Int 类型
    var anotherVariable = "World"; // 编译器推断为 String 类型
    ```
3.  可变与不可变变量：

    * 默认情况下，使用 `var` 声明的变量是可变的，可以在后续代码中被重新赋值。

    ```haxe
    var mutableVar = 5;
    mutableVar = 10;
    ```

    * 如果要声明不可变变量，可以使用 `var` 并结合 `final` 关键字或者直接使用 `final var`。一旦被初始化，不可变变量就不能再被重新赋值。

    ```haxe
    final var immutableVar = 7;
    // immutableVar = 12; // 会导致编译错误
    final var anotherImmutable = "Some text";
    ```
4.  数组变量声明：

    * 明确类型的数组声明：

    ```haxe
    var intArray:Array<Int> = [1, 2, 3];
    ```

    * 类型推断的数组声明：

    ```haxe
    var inferredArray = [4, 5, 6]; // 编译器推断为 Array<Int> 类型
    ```
5.  映射（字典）变量声明：

    * 明确类型的映射声明：

    ```haxe
    var myMap:Map<String,Int> = {'key1': 10, 'key2': 20};
    ```

    * 类型推断的映射声明：

    ```haxe
    var inferredMap = {'key3': 30, 'key4': 40}; // 编译器推断为 Map<String,Int> 类型
    ```



## 小结

{% hint style="info" %}
1、 使用var声明变量

2、final  var 生命常量
{% endhint %}
