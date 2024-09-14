# 函数/方法

在 Objective-C 中，“函数”和“方法”有一些区别：

**一、函数**

&#x20;使用了C语言中的函数



**二、方法**

1. 定义：
   * 方法是与类或对象相关联的函数。
   * 定义在类的接口（`.h`文件）和实现（`.m`文件）中。
2.  语法：

    * 分为实例方法和类方法。
    * 实例方法的语法是 `- (返回类型)方法名:(参数类型)参数名;`，可以访问实例变量。例如：

    ```objective-c
    @interface MyClass : NSObject
    {
        int instanceVariable;
    }
    - (void)myInstanceMethod:(int)param;
    @end
    ```

    * 类方法的语法是 `+(返回类型)方法名:(参数类型)参数名;`，不能访问实例变量，通常用于创建对象或执行与类相关的操作。例如：

    ```objective-c
    @interface MyClass : NSObject
    + (void)myClassMethod:(int)param;
    @end
    ```
3. 调用方式：
   * 实例方法通过对象来调用。例如：`MyClass *obj = [[MyClass alloc] init]; [obj myInstanceMethod:10];`。
   * 类方法通过类名来调用。例如：`[MyClass myClassMethod:20];`。
