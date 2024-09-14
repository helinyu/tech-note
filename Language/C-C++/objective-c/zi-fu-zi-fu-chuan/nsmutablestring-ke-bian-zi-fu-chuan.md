# NSMutableString（可变字符串）

`NSMutableString`是 Objective-C 中用于表示可变字符串的类，它继承自`NSString`。

**一、属性**

一般来说，`NSMutableString`没有公开的可直接设置的属性，它的属性主要是通过方法进行操作得到的，比如字符串的长度可以通过`length`方法获取。

**二、方法**

1. 创建方法：
   * `+ (instancetype)stringWithCapacity:(NSUInteger)capacity`：创建一个具有指定初始容量的可变字符串对象。
2. 追加和插入方法：
   * `appendString:(NSString *)aString`：在当前字符串的末尾追加一个字符串。
   * `insertString:(NSString *)aString atIndex:(NSUInteger)loc`：在指定索引位置插入一个字符串。
3. 删除方法：
   * `deleteCharactersInRange:(NSRange)range`：删除指定范围内的字符。
4. 替换方法：
   * `replaceCharactersInRange:(NSRange)range withString:(NSString *)aString`：用给定的字符串替换指定范围内的字符。
5. 其他常用方法：
   * `setString:(NSString *)aString`：将可变字符串设置为给定的字符串，相当于重新初始化。
   * `appendFormat:(NSString *)format,...`：类似于`NSString`的`stringWithFormat:`，但会在可变字符串末尾追加格式化后的字符串。

**三、内容特点**

1. 可变性：与不可变的`NSString`不同，`NSMutableString`的内容可以在创建后被修改、添加、删除或替换。
2. 动态调整大小：随着字符串内容的变化，`NSMutableString`可以自动调整其内部存储的大小，以适应不断变化的字符串长度。
3. 与`NSString`的兼容性：由于继承自`NSString`，可以在需要`NSString`的地方使用`NSMutableString`对象，不过这样使用时它将表现为不可变字符串。同时，也可以将不可变的`NSString`转换为`NSMutableString`进行修改。
