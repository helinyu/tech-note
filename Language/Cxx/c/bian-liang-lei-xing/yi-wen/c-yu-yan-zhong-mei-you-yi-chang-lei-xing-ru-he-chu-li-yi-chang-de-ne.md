# C语言中没有异常类型，如何处理异常的呢？

在 C 语言中没有像 C++、Java 等语言那样的内置异常处理机制，但可以通过以下几种方式来处理错误情况：

1. 返回错误码：
   * 函数可以返回特定的错误码来表示出现了错误。例如，标准 C 库中的很多函数在出错时会返回特定的负值（如 `perror`、`strtol` 等）或者 `NULL`（如 `malloc` 在分配内存失败时）。
   * 调用者需要检查函数的返回值，并根据返回值进行相应的处理。
2.  使用 `errno`：

    * `errno` 是一个全局变量，用于存储最近一次错误的错误码。许多标准 C 函数在出错时会设置 `errno` 的值。
    * 可以使用 `perror` 函数根据 `errno` 的值打印错误信息。例如：

    ```c
    #include <stdio.h>
    #include <errno.h>

    int main() {
        FILE *fp = fopen("nonexistent.txt", "r");
        if (fp == NULL) {
            perror("Error opening file");
            return 1;
        }
        return 0;
    }
    ```
3.  长跳转（`setjmp`/`longjmp`）：

    * `setjmp` 和 `longjmp` 函数可以实现非局部跳转。可以在一个函数中设置跳转点（通过 `setjmp`），在其他函数中出现错误时进行长跳转回到设置的跳转点进行错误处理。
    * 这种方式使用起来比较复杂，并且可能会破坏程序的正常结构和资源管理，所以要谨慎使用。

    ```c
    #include <stdio.h>
    #include <setjmp.h>

    jmp_buf env;

    void someFunction() {
        // Some error occurs.
        longjmp(env, 1);
    }

    int main() {
        if (setjmp(env) == 0) {
            someFunction();
        } else {
            printf("Error occurred.\n");
        }
        return 0;
    }
    ```
