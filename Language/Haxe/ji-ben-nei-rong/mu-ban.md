# 模板

在 Haxe 中，模板（Templates）是一种强大的语言特性，它允许你创建可复用的代码结构，并在运行时动态生成代码。

**一、字符串模板（String Interpolation）**

Haxe 支持在字符串中使用 `${expression}` 的方式来插入变量或表达式的值。

```haxe
var name = "John";
var age = 30;
trace("My name is ${name} and I am ${age} years old.");
```

这将输出：`My name is John and I am 30 years old.`

**二、类模板（Class Templates）**

1.  泛型类模板：

    ```haxe
    class MyClass<T> {
        var value:T;

        public function new(v:T) {
            value = v;
        }
    }

    var myIntClass = new MyClass<Int>(10);
    var myStringClass = new MyClass<String>("Hello");
    ```
2.  扩展类模板：

    ```haxe
    class BaseClass {
        public function sayHello() {
            trace("Hello from BaseClass");
        }
    }

    class DerivedClass<T> extends BaseClass {
        var value:T;

        public function new(v:T) {
            value = v;
        }
    }

    var derived = new DerivedClass<String>("Hi");
    derived.sayHello();
    ```

**三、函数模板（Function Templates）**

1.  泛型函数模板：

    ```haxe
    function add<T>(a:T, b:T):T {
        return cast a + b;
    }

    trace(add(10, 20));
    trace(add("Hello", " World"));
    ```
2.  可变参数函数模板：

    ```haxe
    function sum(...args:Int):Int {
        var total = 0;
        for (arg in args) {
            total += arg;
        }
        return total;
    }

    trace(sum(1, 2, 3, 4, 5));
    ```

模板使得 Haxe 代码更加灵活和可复用，能够适应不同的数据类型和场景。



{% hint style="info" %}
小结

1、字符串模板， 就是字符串的内容搞成的模板，类似Vue3中的模板，可以算是一个字符串模板

2、函数模板、类模板 ， 就是C++中的模板

3、所以：Vue和C++中的模板的区别就是一个是字符串模板，一个是函数/类模板


{% endhint %}



