# NSString（不可变字符串）

在 Objective-C 中，`NSString`类代表字符串，它具有以下一些主要的属性、方法和内容特点：

**一、属性**

`NSString`本身没有公开的可直接设置的属性，但它具有一些特性：

* 不可变性：一旦创建，其内容不能被直接修改。例如，不能像对普通的 Objective-C 对象那样直接修改其属性来改变字符串的内容。

**二、方法**

1. 创建字符串的方法：
   * `+ (instancetype)stringWithFormat:(NSString *)format,...`：使用格式化字符串创建`NSString`对象。
   * `+ (instancetype)stringWithUTF8String:(const char *)nullTerminatedCString`：从 C 风格的以空字符结尾的字符串创建`NSString`对象。
2. 字符串操作方法：
   * 拼接字符串：
     * `- (instancetype)stringByAppendingString:(NSString *)aString`：在当前字符串末尾追加另一个字符串。
   * 比较字符串：
     * `- (NSComparisonResult)compare:(NSString *)string`：比较两个字符串，返回比较结果。
   * 获取子字符串：
     * `- (NSString *)substringFromIndex:(NSUInteger)from`：从指定索引开始获取子字符串。
     * `- (NSString *)substringToIndex:(NSUInteger)to`：获取从字符串开头到指定索引的子字符串。
     * `- (NSString *)substringWithRange:(NSRange)range`：根据指定范围获取子字符串。
   * 查找字符串：
     * `- (NSRange)rangeOfString:(NSString *)searchString`：查找指定字符串在当前字符串中的位置。
   * 转换方法：
     * `- (const char *)UTF8String`：将`NSString`对象转换为 C 风格的以空字符结尾的 UTF-8 编码字符串。
     * `- (NSUInteger)length`：获取字符串的长度。

**三、内容特点**

1. 存储方式：
   * `NSString`以高效的方式存储字符串内容，通常使用 Unicode 编码来支持多种语言字符。
2. 不可变性的优势：
   * 由于不可变，多个对象可以共享相同的字符串内容，节省内存。
   * 在多线程环境下更安全，不需要担心被其他线程意外修改。
3. 与其他类型的交互：
   * 可以方便地与其他 Objective-C 对象进行交互，例如作为方法的参数或返回值。
   * 可以与基本数据类型进行转换，如使用`stringWithFormat:`方法将数字等基本数据类型转换为字符串。
