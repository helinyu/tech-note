---
description: 这个经常会用到在数学上
---

# 数学常量(Math库)

## 特殊的数据类型以及常量

* NaN (Not a Number): returned when a mathematically incorrect operation is executed, e.g. Math.sqrt(-1) 这个是一个数字
* POSITIVE\_INFINITY:  最大值
* NEGATIVE\_INFINITY: 最小资
* PI : 3.1415... π

。。。。

将浮点数转化为整数

**Std.int()**&#x20;



**对Math库的扩展**

```
class MathStaticExtension {
  /* Converts an angle in radians to degrees */
  inline public static function toDegrees(radians:Float):Float {
    return radians * 180 / Math.PI;
  }
}
using MathStaticExtension;

class Main {
  public static function main() {
    var ang = 1 / 2 * Math.PI;
    trace(ang.toDegrees()); // 90
  }
}
```
