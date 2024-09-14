# json

在 Haxe 中，可以方便地处理 JSON（JavaScript Object Notation）数据。

**一、将对象转换为 JSON 字符串**

可以使用 `haxe.Json.stringify()` 方法将一个对象转换为 JSON 字符串。

```haxe
import haxe.Json;

class Person {
    public var name:String;
    public var age:Int;

    public function new(name:String, age:Int) {
        this.name = name;
        this.age = age;
    }
}

var p = new Person("John", 30);
var jsonString = Json.stringify(p);
trace(jsonString);
```

**二、将 JSON 字符串转换为对象**

使用 `haxe.Json.parse()` 方法可以将 JSON 字符串转换为一个对象。

```haxe
var jsonStr = '{"name":"Jane","age":25}';
var obj = Json.parse(jsonStr);
if (obj!= null) {
    trace(cast obj.name);
    trace(cast obj.age);
}
```

**三、处理复杂的 JSON 结构**

1. 处理数组：

```haxe
var jsonArrayStr = '[{"name":"John","age":30},{"name":"Jane","age":25}]';
var arrayObj = Json.parse(jsonArrayStr);
if (arrayObj!= null && arrayObj.arr!= null) {
    for (item in arrayObj.arr) {
        trace(cast item.name);
        trace(cast item.age);
    }
}
```

2. 嵌套对象：

```haxe
var nestedJsonStr = '{"person":{"name":"John","age":30},"address":{"city":"New York"}}';
var nestedObj = Json.parse(nestedJsonStr);
if (nestedObj!= null) {
    var person = cast nestedObj.person;
    trace(person.name);
    trace(person.age);
    var address = cast nestedObj.address;
    trace(address.city);
}
```

Haxe 的 JSON 处理功能使得在不同平台上进行数据交换和存储变得更加容易。
