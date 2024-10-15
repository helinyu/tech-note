# onExit概念

C语言本身并没有 `@onExit` 这样的语法，但可以通过一些技巧实现类似的功能，特别是使用 `__attribute__((cleanup))` 或编写自定义宏来在作用域结束时执行特定的清理操作。下面是一些实现 `@onExit` 效果的常见方法：

#### 方法 1：使用 `__attribute__((cleanup))`

GCC 和 Clang 提供了 `__attribute__((cleanup))`，它允许我们在变量离开作用域时自动调用一个清理函数。这类似于在作用域结束时执行代码，模拟了 `@onExit` 的效果。

```c
#include <stdio.h>

void cleanup(int *p) {
    printf("Cleaning up: %d\n", *p);
}

int main() {
    int x __attribute__((cleanup(cleanup))) = 10;
    printf("In function, x = %d\n", x);
    return 0;
}
```

**说明**：

* `x` 离开作用域时会调用 `cleanup` 函数，自动输出 "Cleaning up" 信息。
* `cleanup` 函数的参数是变量的地址，因此我们可以访问并修改变量的值。

#### 方法 2：编写 `defer` 宏

可以编写一个 `defer` 宏，在作用域结束时执行清理代码。这个宏的原理是使用 C 的“作用域和栈帧特性”在作用域结束时执行清理代码。

```c
#include <stdio.h>

#define CONCAT(a, b) a##b
#define DEFER_ID(line) CONCAT(defer_, line)
#define defer __attribute__((cleanup(defer_cleanup))) void (*DEFER_ID(__LINE__))(void) = 

void defer_cleanup(void (^*block)(void)) {
    (*block)();
}

void cleanup_task() {
    printf("Deferred cleanup\n");
}

int main() {
    defer ^{ cleanup_task(); };
    printf("In function\n");
    return 0;
}
```

**说明**：

* `defer` 宏使用了 `__attribute__((cleanup))` 和一个闭包来延迟执行指定代码。
* `defer` 的效果类似于 `@onExit` 或 Swift 的 `defer`，在作用域结束时自动执行清理操作。

#### 方法 3：使用 `atexit` 注册退出函数

在 C 标准库中，`atexit` 函数可以注册一个程序结束时调用的函数。虽然它不能在作用域结束时执行，但适用于在程序退出时需要执行的清理操作。

```c
#include <stdio.h>
#include <stdlib.h>

void cleanup() {
    printf("Program exiting, cleaning up resources.\n");
}

int main() {
    atexit(cleanup);
    printf("In function\n");
    return 0;
}
```

**说明**：

* `atexit` 注册的 `cleanup` 函数会在 `main` 返回或调用 `exit` 时执行。
* 适用于全局资源的清理，不适用于局部作用域的清理。
