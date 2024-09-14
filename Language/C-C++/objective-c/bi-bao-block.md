# 闭包/block

在 OC（Objective-C）中，闭包（Block）是一种捕获周围上下文并能在以后执行的代码段。它与其他编程语言中的闭包概念类似，比如 Swift 中的闭包或 C++ 中的 lambda 表达式。

#### Block 的定义和使用

闭包通常通过 `^` 符号定义，形式如下：

```objective-c
returnType (^blockName)(parameterTypes) = ^returnType(parameters) {
    // Code to execute
};
```

**示例**

```objective-c
int (^sumBlock)(int, int) = ^int(int a, int b) {
    return a + b;
};

int result = sumBlock(3, 5); // result 是 8
```

**简单使用：**

1.  **无参数、无返回值的 Block**

    ```objective-c
    void (^simpleBlock)(void) = ^{
        NSLog(@"这是一个简单的 Block");
    };
    simpleBlock();  // 执行 Block
    ```
2.  **带参数和返回值的 Block**

    ```objective-c
    int (^multiplyBlock)(int, int) = ^int(int a, int b) {
        return a * b;
    };
    int result = multiplyBlock(3, 4);  // result 是 12
    ```

#### Block 捕获变量

Block 会自动捕获它所定义时周围的局部变量，并且可以在执行时访问这些变量。需要注意的是，默认情况下，Block 捕获的局部变量是只读的。

```objective-c
int multiplier = 10;
int (^multiplyBlock)(int) = ^int(int num) {
    return num * multiplier; // 捕获了 multiplier 变量
};
int result = multiplyBlock(5); // result 是 50
```

如果你希望在 Block 中修改捕获的局部变量，需要将其声明为 `__block` 修饰符。

```objective-c
__block int multiplier = 10;
int (^multiplyBlock)(int) = ^int(int num) {
    multiplier += 5; // 可以修改 multiplier
    return num * multiplier;
};
int result = multiplyBlock(5);  // multiplier 被修改为 15，result 是 75
```

#### Block 内存管理

Objective-C 中的 Block 分为三类：

1. **栈上的 Block**：定义在函数或方法中的 Block 默认是栈上的。当函数或方法结束时，栈上的 Block 就会被销毁。
2. **堆上的 Block**：当你需要在函数或方法之外执行 Block 时，栈上的 Block 会被复制到堆上。通过 `Block_copy` 或者在函数外使用的情况下，系统会自动将 Block 从栈复制到堆上。
3. **全局 Block**：如果 Block 没有捕获任何外部变量，它会被当作全局的 Block。

```objective-c
int (^block)(int) = ^int(int num) {
    return num * 5;
};

block = [block copy]; // 将 Block 从栈复制到堆上
```

#### Block 与 GCD 的结合

Block 在 GCD（Grand Central Dispatch）中大量使用，特别是用于并发编程。以下是一个简单的异步执行任务的示例：

```objective-c
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    NSLog(@"在后台线程执行任务");
    dispatch_async(dispatch_get_main_queue(), ^{
        NSLog(@"回到主线程更新 UI");
    });
});
```

通过 Block，OC 实现了简洁而强大的闭包功能，非常适合异步任务、回调处理等。
