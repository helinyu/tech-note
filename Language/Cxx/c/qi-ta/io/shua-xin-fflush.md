# fflush

<mark style="color:red;">`fflush`</mark><mark style="color:red;">函数用于清空输出缓冲区，将缓冲区中的数据强制写入到目标文件或设备</mark>。其主要用途和特性如下：

#### 1. **语法**

```c
int fflush(FILE *stream);
```

#### 2. **参数**

* `stream`：指向`FILE`对象的指针，代表要刷新的输出流。如果参数为`NULL`，则会刷新所有输出流的缓冲区。

#### 3. **返回值**

* 成功时返回0，失败时返回EOF，并设置`errno`以指示错误原因。

#### 4. **使用场景**

* **输出到终端**：在终端程序中，确保输出立即显示，而不是等待缓冲区满。
* **文件写入**：在进行文件操作时，确保数据在程序崩溃或异常退出前被写入文件。
* **交互式程序**：在需要及时响应用户输入时，确保输出内容可见。

#### 5. **注意事项**

* 对于输入流，调用`fflush`是未定义的行为，通常不推荐使用。
* 使用`fflush`时要小心，频繁调用可能影响性能，因为它会导致I/O操作。

#### 示例代码

```c
#include <stdio.h>

int main() {
    printf("Hello, World!");
    fflush(stdout); // 确保内容立即输出到终端

    FILE *file = fopen("output.txt", "w");
    if (file) {
        fprintf(file, "Writing to file...\n");
        fflush(file); // 强制写入文件
        fclose(file);
    }

    return 0;
}
```

在这个示例中，`fflush(stdout)`确保`printf`的输出立即可见，而`fflush(file)`确保数据写入到文件。



#### 详细使用场景

1. **缓冲区行为**
   * 默认情况下，标准输出（如`stdout`）通常是行缓冲的，这意味着在输出换行符时，缓冲区会被刷新。使用`fflush(stdout)`可以手动刷新，即使没有换行符。
2. **文件操作**
   * 在写入文件时，尤其是在进行多次写入后，使用`fflush`可以确保数据立即写入文件，而不是等待缓冲区满或文件关闭时才写入。
3. **网络编程**
   * 在网络编程中，确保数据被及时发送到网络套接字，可以使用`fflush`。

#### 代码示例

**例子 1：行缓冲和手动刷新**

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    printf("Waiting for input...\n");
    fflush(stdout); // 强制输出到终端

    // 等待用户输入
    sleep(5); // 模拟等待
    printf("Input received!\n");

    return 0;
}
```

在这个例子中，`fflush(stdout)`确保“Waiting for input...”在等待用户输入之前立即输出。

**例子 2：文件写入**

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "w");
    if (file) {
        fprintf(file, "First line.\n");
        fflush(file); // 立即写入文件

        fprintf(file, "Second line.\n");
        fflush(file); // 再次立即写入
        fclose(file);
    } else {
        perror("Error opening file");
    }
    return 0;
}
```

这里，`fflush(file)`确保每次写入后数据立即写入到`example.txt`。

#### 注意事项

* 使用`fflush`时要避免对输入流（如`stdin`）调用，它会导致未定义行为。
* 频繁调用`fflush`可能影响程序性能，因此在需要时合理使用。

