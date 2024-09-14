# 变量类型

Haxe 是一门 **静态类型** 编程语言，意味着每个变量在编译时都有一个确定的类型，编译器可以对类型进行检查。Haxe 提供了多种变量类型，涵盖了基本类型、复杂类型、用户自定义类型等。同时，Haxe 支持 **类型推断**，所以开发者在某些情况下不必显式声明变量的类型，编译器会自动推断。

#### 1. **基本类型**

*   **Int**：整数类型，通常是 32 位整数。

    ```haxe
    var a:Int = 10;
    ```
*   **Float**：浮点数类型，用于存储小数。

    ```haxe
    var b:Float = 3.14;
    ```
*   **Bool**：布尔类型，表示 `true` 或 `false`。

    ```haxe
    var isTrue:Bool = true;
    ```
*   **String**：字符串类型，存储文本。

    ```haxe
    var str:String = "Hello, Haxe!";
    ```
*   **Null\<T>**：可以为空的类型，`Null` 类型允许值为 `null`。在某些平台（如 JavaScript 和 PHP），所有类型都可以为空；在其他平台（如 C++），只有 `Null<T>` 类型可以为空。

    ```haxe
    var nullable:Int = null;
    var nonNullable:Null<Int> = null;
    ```

#### 2. **复杂类型**

*   **Array\<T>**：数组类型，存储相同类型的元素。

    ```haxe
    var numbers:Array<Int> = [1, 2, 3, 4];
    ```
*   **Map\<K, V>**：键值对映射，允许通过键来访问值。键和值可以是不同的类型。

    ```haxe
    var map:Map<String, Int> = ["one" => 1, "two" => 2];
    ```
*   **Enum**：枚举类型，用于表示一组固定的常量，类似于其他语言中的枚举。Haxe 的枚举比传统枚举更强大，可以包含带参数的值。

    ```haxe
    enum Color {
      Red;
      Green;
      Blue;
      Custom(rgb:Int);
    }

    var c:Color = Color.Red;
    ```
*   **Class**：Haxe 支持面向对象编程，类是一种复杂类型，可以定义属性和方法。

    ```haxe
    class Person {
      public var name:String;
      public function new(name:String) {
        this.name = name;
      }
    }

    var p:Person = new Person("Alice");
    ```

#### 3. **其他类型**

*   **Dynamic**：动态类型，可以容纳任意类型的值。`Dynamic` 通常用于需要在运行时确定类型的场景，比如从外部 API 获取的数据。

    ```haxe
    var dynVar:Dynamic = "Hello"; // 之后可以变为其他类型
    dynVar = 123;
    ```
*   **Function**：函数类型，表示函数的输入和输出。Haxe 中的函数本身是第一类对象，可以赋值给变量或传递给其他函数。

    ```haxe
    var add:Function = function(a:Int, b:Int):Int {
      return a + b;
    };
    trace(add(1, 2)); // 输出: 3
    ```
*   **Void**：表示无返回值的类型，通常用于函数返回值为 `Void` 的场景。

    ```haxe
    function printMessage():Void {
      trace("This is a message");
    }
    ```

#### 4. **结构类型 (Anonymous Structure)**

Haxe 支持匿名结构（类似于 TypeScript 的接口）。它是一种没有显式类定义的对象，可以定义字段和方法。

```haxe
var point = { x: 10, y: 20 };
trace(point.x); // 输出: 10
```

#### 5. **抽象类型 (Abstract Types)**

Haxe 提供了抽象类型，这是一种基于现有类型的封装，可以添加自定义逻辑和限制。抽象类型可以像常规类型一样使用，但允许开发者对其行为进行控制和扩展。

```haxe
abstract MyInt(Int) {
  public function new(i:Int) {
    this = i;
  }
  
  public function add(x:Int):MyInt {
    return new MyInt(this + x);
  }
}

var myValue:MyInt = new MyInt(5);
trace(myValue.add(10)); // 输出: 15
```

#### 6. **类型推断**

Haxe 支持类型推断，编译器可以根据表达式的上下文自动推断出变量的类型。因此，开发者不必总是显式声明变量的类型。

```haxe
var num = 10;        // 编译器推断为 Int
var message = "Hi!"; // 编译器推断为 String
```

#### 7. **Typedef**

**Typedef** 允许为现有的复杂类型定义新的名字，并可以定义更复杂的数据结构，比如嵌套的对象和函数类型。

```haxe
typedef Person = {
  var name:String;
  var age:Int;
};

var p:Person = { name: "John", age: 25 };
trace(p.name); // 输出: John
```

#### 8. **联合类型**

Haxe 支持在特定场景下使用联合类型，表示一个值可以是多种类型中的一种。

```haxe
var val:IntOrString = 5;
val = "Hello";
```

联合类型可以通过枚举或抽象类型来实现。

#### 总结

Haxe 提供了强大且灵活的类型系统，支持从基本类型到复杂类型的多种定义方式。通过静态类型和类型推断的结合，Haxe 在编译时能够进行严格的类型检查，同时保持代码的简洁性。此外，Haxe 的复杂类型如 `Enum` 和 `Abstract` 提供了对数据建模的强大能力，使其在多平台开发中非常灵活。
