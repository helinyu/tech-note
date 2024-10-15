# C语言中onExit的定义

在 C 语言中，`onExit` 并不是一个内置的关键字或功能，但是可以通过使用 GCC 或 Clang 提供的 `__attribute__((cleanup))` 属性来实现类似的效果。`__attribute__((cleanup))` 允许在变量离开作用域时调用一个自定义的清理函数。基于此，我们可以创建一个宏 `onExit`，在退出作用域时执行清理操作。

#### C 语言中 `onExit` 的定义

以下是一个 C 语言中 `onExit` 的实现示例。这个宏使用 `__attribute__((cleanup))`，可以确保在代码块退出时调用指定的清理函数。

```c
#include <stdio.h>

typedef void (*cleanup_func_t)(void *);

#define onExit \
    __attribute__((cleanup(cleanup_function))) cleanup_func_t on_exit_function = (void (*)(void *))^

void cleanup_function(cleanup_func_t *func) {
    if (func && *func) {
        (*func)(NULL);  // 调用清理函数
    }
}

int main() {
    onExit {
        printf("Exiting the scope!\n");
    };

    printf("In the main function\n");

    return 0;
}
```

#### 解释

1. **`cleanup_func_t`**\
   `cleanup_func_t` 是一个函数指针类型，定义为 `void (*cleanup_func_t)(void *)`，用于指向清理函数。
2. **`onExit` 宏**\
   `onExit` 宏使用了 `__attribute__((cleanup(cleanup_function)))`，这会在变量离开作用域时调用 `cleanup_function`，并传入 `on_exit_function` 指向的 block（即清理代码块）。
3. **`cleanup_function`**\
   `cleanup_function` 是一个负责调用清理代码的函数。在作用域结束时，它会被自动调用，并执行 `onExit` 指定的代码。
4. **`main` 函数中的用法**\
   `onExit` 宏展开后，`printf("Exiting the scope!\n");` 将在 `main` 函数结束时自动执行，实现了类似 `defer` 的效果。

#### 预处理展开

在 `main` 函数中使用 `onExit` 时，预处理器会将其展开为如下代码：

```c
__attribute__((cleanup(cleanup_function))) cleanup_func_t on_exit_function = (void (*)(void *))^{
    printf("Exiting the scope!\n");
};
```

#### 运行效果

此代码运行时，将输出：

```plaintext
In the main function
Exiting the scope!
```

在 `main` 函数退出之前，`onExit` 宏中定义的代码块会被调用，打印 `"Exiting the scope!"`。
