# \_\_attribute\_\_

<mark style="color:red;">`__attribute__`</mark> <mark style="color:red;"></mark><mark style="color:red;">是 GCC 和 Clang 编译器提供的一个编译器扩展，用于给变量、函数或类型添加特殊属性（attributes），从而影响编译器对它们的处理方式</mark>。在 C 和 Objective-C 中，`__attribute__` 可以用于设置特定编译行为，比如函数的优化方式、内存对齐、清理代码等。

#### `__attribute__` 的常见用途

1.  **`__attribute__((cleanup))`**：在变量作用域结束时自动调用指定的清理函数。常用于资源管理，比如自动释放内存、文件关闭等。

    ```c
    void cleanup_function(int *p) {
        printf("Cleaning up!\n");
        *p = 0;
    }

    void example() {
        int x __attribute__((cleanup(cleanup_function))) = 10;
        // 作用域结束时会调用 cleanup_function(&x)
    }
    ```
2.  **`__attribute__((deprecated))`**：标记函数或变量为过时，使用时编译器会发出警告。这在提醒开发者避免使用老旧接口时很有用。

    ```c
    int old_function() __attribute__((deprecated));
    ```
3.  **`__attribute__((aligned))`**：指定变量或结构体的内存对齐方式，以提升内存访问效率或满足特定的硬件要求。

    ```c
    struct __attribute__((aligned(16))) AlignedStruct {
        int data[4];
    };
    ```
4.  **`__attribute__((noreturn))`**：用于标记不返回值的函数，例如直接退出程序的函数。编译器会据此优化代码。

    ```c
    void exit_now() __attribute__((noreturn));
    ```
5.  **`__attribute__((format))`**：帮助编译器检测格式化函数（如 `printf`）中的格式化错误。这对于自定义格式化输出函数尤其有用。

    ```c
    void my_printf(const char *format, ...) __attribute__((format(printf, 1, 2)));
    ```

#### 语法

`__attribute__` 的一般形式为：`__attribute__((attribute_list))`，其中 `attribute_list` 是逗号分隔的属性列表，作用的代码元素可以是函数、变量、类型或结构体等。
