# 字符/字符串

在 Objective-C（OC）中，字符和字符串有以下特点：

**一、字符（`char`）**

1. 定义：
   * `char`类型用于表示单个字符，通常占用 1 个字节的内存空间。
   * 例如：`char c = 'A';`。
2. 字符常量：
   * 可以使用单引号括起来的单个字符作为字符常量，如`'a'`、`'B'`等。
   * 也可以使用转义字符，如`'\n'`表示换行符，`'\t'`表示制表符等。
3. ASCII 值：
   * 字符在内存中实际上是以 ASCII 值的形式存储的。
   * 可以通过将字符强制转换为整数来获取其 ASCII 值，例如：`int asciiValue = (int)'A';`。

**二、字符串（`NSString`和`char *`）**

1. `NSString`对象：
   * `NSString`是 Objective-C 中用于表示字符串的类。
   * 创建方式：
     * 字面量创建：`NSString *str = @"Hello, World!";`。
     * 使用类方法创建：`NSString *str2 = [NSString stringWithFormat:@"Number: %d", 10];`。
   * 特点：
     * 是不可变字符串，一旦创建后内容不能被修改。如果需要修改字符串内容，可以创建一个新的`NSString`对象。
     * 提供了丰富的方法用于字符串的操作，如拼接、查找、比较等。
2. `char *`字符串：
   * C 风格的字符串，以`'\0'`（空字符）作为结束标志。
   * 例如：`char *str3 = "Hello";`。
   * 特点：
     * 可以通过指针操作修改字符串内容，但需要注意内存管理问题，避免内存泄漏和越界访问。
     * 与`NSString`相比，功能相对简单，没有那么多高级的字符串操作方法。
3. 相互转换：
   * `NSString`转`char *`：可以使用`UTF8String`方法将`NSString`对象转换为 C 风格的字符串。例如：`const char *cStr = [str UTF8String];`。
   * `char *`转`NSString`：可以使用`initWithUTF8String:`方法将 C 风格的字符串转换为`NSString`对象。例如：`NSString *str4 = [[NSString alloc] initWithUTF8String:cStr];`。
