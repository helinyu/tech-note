# 系列化

在 Haxe 中，序列化（serialization）是将对象转换为可以存储或传输的格式，以及从这种格式恢复对象的过程。Haxe 提供了一些方式来实现序列化。

**一、使用 haxe.Serializer 和 haxe.Unserializer**

1.  序列化：

    ```haxe
    import haxe.Serializer;
    import haxe.Unserializer;

    class Person {
        public var name:String;
        public var age:Int;

        public function new(name:String, age:Int) {
            this.name = name;
            this.age = age;
        }
    }

    var p = new Person("John", 30);
    var s = new Serializer();
    s.serialize(p);
    var bytes = s.getBytes();
    ```
2.  反序列化：

    ```haxe
    var us = new Unserializer(bytes);
    var restoredPerson = us.unserialize();
    trace(cast restoredPerson.name);
    trace(cast restoredPerson.age);
    ```

**二、特定平台的序列化方式**

在某些目标平台上，可能有特定的序列化库或机制可用。例如，在 JavaScript 目标中，可以使用 JSON.stringify 和 JSON.parse 进行简单的序列化和反序列化。

**注意事项**：

* 序列化和反序列化的对象需要满足一定的条件，例如对象的字段必须是可序列化的类型，并且对象的结构在序列化和反序列化过程中不能发生变化。
* 序列化可能存在安全风险，特别是当处理来自不可信来源的数据时，需要谨慎处理以防止潜在的安全漏洞。

