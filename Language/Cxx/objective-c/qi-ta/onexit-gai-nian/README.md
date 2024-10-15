# onExit概念



{% code overflow="wrap" %}
```
#define onExit \
    rac_keywordify \
    __strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^


    
#if DEBUG
#define rac_keywordify autoreleasepool {}
#else
#define rac_keywordify try {} @catch (...) {}
#endif

/*** implementation details follow ***/
typedef void (^rac_cleanupBlock_t)(void);

static inline void rac_executeCleanupBlock (__strong rac_cleanupBlock_t *block) {
    (*block)();
}

#define metamacro_concat(A, B) \
        metamacro_concat_(A, B)

#define metamacro_concat_(A, B) A ## B

```
{% endcode %}



这个 `#define onExit` 宏定义通过 `__attribute__((cleanup))` 和 `^` 块（block）实现了一种类似于 `@onExit` 的功能，在代码块退出时自动执行清理操作。我们可以逐步理解该宏的组成部分：

```objective-c
#define onExit \
    rac_keywordify \
    __strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^
```

#### 宏的各个部分解析

1. **`rac_keywordify`**
   * 这是一个宏，用于在调试模式和发布模式下使宏的行为一致。它通常定义为 `do {} while (0)`，不会执行任何操作，但可以确保宏的可读性和安全性。
2. **`__strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__)`**
   * `rac_cleanupBlock_t` 是一个自定义类型（通常是 `void (^rac_cleanupBlock_t)(void)`），表示清理操作的 block。
   * `metamacro_concat(rac_exitBlock_, __LINE__)` 通过宏 `metamacro_concat` 将 `rac_exitBlock_` 和当前代码行号连接在一起，**形成唯一的变量名**，以避免命名冲突。
   * `__LINE__` 是一个预定义的宏，表示当前行号。
3. **`__attribute__((cleanup(rac_executeCleanupBlock), unused))`**
   * `cleanup` 是 GCC 和 Clang 的扩展属性，指定在变量离开作用域时调用的清理函数。这里 `rac_executeCleanupBlock` 是一个函数指针，指向执行清理的函数。
   * `unused` 属性告诉编译器，变量可能不被显式使用，不要因此产生警告。
4. **`= ^`**
   * 这个 `= ^` 定义了一个 block（类似匿名函数），用于在当前作用域结束时执行。
   * 因为 `onExit` 宏在展开时最后以 `= ^` 结尾，因此后续代码可以立即书写 `{}` 来指定 block 的实现。

#### 使用示例

利用该宏，可以方便地在方法或作用域结束时执行一些清理操作：

```objective-c
#import <Foundation/Foundation.h>

void rac_executeCleanupBlock(__strong void (^*block)(void)) {
    if (block && *block) {
        (*block)();
    }
}

typedef void (^rac_cleanupBlock_t)(void);

#define onExit \
    rac_keywordify \
    __strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^

int main() {
    @autoreleasepool {
        onExit {
            NSLog(@"Cleaning up resources at scope exit!");
        };

        NSLog(@"Performing operations in the scope...");
    }
    return 0;
}
```

#### 解释

* 在 `main` 的 `@autoreleasepool` 块中，`onExit` 会注册一个在退出作用域时执行的清理操作。在此例中，`NSLog(@"Cleaning up resources at scope exit!");` 将会在 `@autoreleasepool` 块退出时执行。
* `onExit` 提供了一种优雅的方式确保代码块退出时自动进行资源清理，特别适用于需要手动释放的资源管理或调试信息记录。

***

## 展开上面的宏

假设我们有以下代码，使用了 `onExit` 宏：

```objective-c
#import <Foundation/Foundation.h>

#define rac_keywordify autoreleasepool {}
#define metamacro_concat(A, B) A ## B
typedef void (^rac_cleanupBlock_t)(void);

void rac_executeCleanupBlock(__strong rac_cleanupBlock_t *block) {
    if (block && *block) {
        (*block)();
    }
}

#define onExit \
    rac_keywordify \
    __strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^

int main() {
    onExit {
        NSLog(@"Exiting the scope!");
    };
    
    NSLog(@"In the main function");
    return 0;
}
```

在预处理阶段，这段代码将会展开宏定义，将 `onExit` 预处理成具体的代码。接下来让我们看看每一步的展开结果。

#### Step 1: 展开 `onExit`

首先，`onExit` 宏展开为：

```objective-c
rac_keywordify
__strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^
```

#### Step 2: 展开 `rac_keywordify`

根据 `#define rac_keywordify autoreleasepool {}`, `rac_keywordify` 展开为 `autoreleasepool {}`：

```objective-c
autoreleasepool {}
__strong rac_cleanupBlock_t metamacro_concat(rac_exitBlock_, __LINE__) __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^
```

#### Step 3: 展开 `metamacro_concat`

`metamacro_concat(rac_exitBlock_, __LINE__)` 用于将 `rac_exitBlock_` 与当前行号拼接在一起，以形成一个唯一的变量名。在此示例中，假设 `onExit` 位于第 20 行，`__LINE__` 将被替换为 20，得到：

```objective-c
autoreleasepool {}
__strong rac_cleanupBlock_t rac_exitBlock_20 __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^
```

#### 最终结果

当我们在 `main` 函数中使用 `onExit` 宏时，预处理器将会将其展开为以下内容：

```objective-c
int main() {
    autoreleasepool {}
    __strong rac_cleanupBlock_t rac_exitBlock_20 __attribute__((cleanup(rac_executeCleanupBlock), unused)) = ^{
        NSLog(@"Exiting the scope!");
    };
    
    NSLog(@"In the main function");
    return 0;
}
```

#### 执行效果

在这个预处理展开后的代码中：

1. `rac_exitBlock_20` 是一个 block，它被标记为 `__attribute__((cleanup(rac_executeCleanupBlock), unused))`，即当 `rac_exitBlock_20` 离开作用域时，将自动调用 `rac_executeCleanupBlock` 函数，并传入 `rac_exitBlock_20`。
2. `rac_executeCleanupBlock` 函数会执行 `rac_exitBlock_20` 中的代码块 `^{ NSLog(@"Exiting the scope!"); }`，从而在 `main` 函数结束时自动打印 `"Exiting the scope!"`。

所以，这样的宏定义可以实现自动清理逻辑，在退出当前作用域时执行指定的 block 代码。



#### rac\_keywordify 会替换称为autoreleasepool {} 是不是很多余？

不多余， 提供了<mark style="color:red;">语法的安全性、编译一致性以及更好的代码结构</mark>

参考rac\_keywordify[rac\_keywordify.md](rac\_keywordify.md "mention")

