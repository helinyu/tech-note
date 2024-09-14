# 变量类型

在 Objective-C（以下简称 OC）中主要有以下几种变量类型：

## **一、基本数据类型**

1. `int`：整数类型，通常占用 4 个字节，表示整数值。例如：`int a = 10;`。
2. `float`：单精度浮点数类型，通常占用 4 个字节，表示小数。例如：`float b = 3.14f;`。
3. `double`：双精度浮点数类型，通常占用 8 个字节，精度比`float`更高。例如：`double c = 3.1415926;`。
4. `char`：字符类型，通常占用 1 个字节，表示单个字符。例如：`char d = 'A';`。
5. `BOOL`：布尔类型，实际上是一种对`typedef signed char BOOL`的定义。通常用`YES`（真）和`NO`（假）表示。例如：`BOOL isTrue = YES;`。

## **二、指针类型**

1. `id`：通用对象指针类型，可以指向任何 Objective-C 对象。例如：`id obj = [[NSObject alloc] init];`。
2. `Class`：指向类对象的指针类型。例如：`Class cls = [NSString class];`。

## **三、对象类型**

1. `NSObject`及其子类：如`NSString`（字符串对象）、`NSArray`（数组对象）、`NSDictionary`（字典对象）等。这些都是 Objective-C 中的常用对象类型，提供了丰富的方法来操作数据。
   * `NSString *str = @"Hello, World!";`
   * `NSArray *array = @[@"apple", @"banana", @"orange"];`
   * `NSDictionary *dict = @{@"name": @"John", @"age": @25};`

## **四、结构体类型**

1. `NSRange`：用于表示范围，包含一个位置和一个长度。例如：`NSRange range = {2, 5};`。
2. `CGRect`：用于表示矩形，包含原点坐标和尺寸。例如：`CGRect rect = CGRectMake(0, 0, 100, 100);`。

## **五、枚举类型**

1.  自定义枚举：

    ```objc
    typedef enum {
        OptionOne,
        OptionTwo,
        OptionThree
    } MyOptions;
    MyOptions option = OptionTwo;
    ```
2.  `NS_ENUM`宏定义的枚举：

    ```objc
    typedef NS_ENUM(NSInteger, MyEnumType) {
        MyEnumValue1,
        MyEnumValue2,
        MyEnumValue3
    };
    MyEnumType enumValue = MyEnumValue2;
    ```
