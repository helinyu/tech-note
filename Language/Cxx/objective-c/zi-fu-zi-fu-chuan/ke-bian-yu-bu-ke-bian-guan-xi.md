# 可变与不可变关系

在 Objective-C 中，字符串分为不可变字符串（`NSString`）和可变字符串（`NSMutableString`）。

**一、不可变字符串（NSString）**

1. 特点：
   * 一旦创建，其内容不能被修改。
   * 多个对象可以安全地共享同一个不可变字符串，因为它们知道这个字符串不会被改变，这有助于提高内存使用效率和多线程环境下的安全性。
2. 示例：

```objective-c
NSString *str1 = @"Hello";
NSString *str2 = str1;
// str1 和 str2 都指向同一个不可变的字符串内容
```

**二、可变字符串（NSMutableString）**

1. 特点：
   * 可以在创建后修改其内容，例如添加、删除或替换字符。
   * 提供了一系列方法来进行这些修改操作。
2. 示例：

```objective-c
NSMutableString *mutableStr = [NSMutableString stringWithString:@"Hello"];
[mutableStr appendString:@" World"];
// mutableStr 现在的内容是 "Hello World"
```

**三、两者的转换**

1. 从不可变字符串创建可变字符串：

```objective-c
NSString *immutableStr = @"Hello";
NSMutableString *mutableCopy = [NSMutableString stringWithString:immutableStr];
```

2. 从可变字符串创建不可变字符串：

```objective-c
NSMutableString *mutableStr = [NSMutableString stringWithString:@"Hello"];
NSString *immutableCopy = [NSString stringWithString:mutableStr];
```

在实际编程中，根据具体的需求选择使用不可变字符串还是可变字符串。如果字符串内容确定不会改变，使用不可变字符串可以提高性能和安全性；如果需要动态修改字符串内容，则使用可变字符串。
