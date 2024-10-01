# fclose

在 C 语言中，`fclose` 函数用于关闭一个打开的文件流。它是标准库 `<stdio.h>` 中的一部分。

#### `fclose` 函数的原型

```c
int fclose(FILE *stream);
```

#### 参数

* **`stream`**：指向要关闭的文件流的指针，这个指针通常是通过 `fopen` 函数获得的。

#### 返回值

* 返回 `0` 表示成功关闭文件。
* 返回 `EOF`（通常是 -1）表示关闭文件失败，并且可以使用 `errno` 检查错误原因。

#### 使用注意事项

* 在完成文件操作后，应该总是调用 `fclose` 以关闭文件。这将释放与文件流相关的资源，并确保所有缓冲区中的数据被写入文件。
* 如果程序在关闭文件时遇到错误，可能会导致数据丢失。因此，检查返回值是一个良好的编程习惯。

#### 示例代码

以下是一个简单的示例，展示如何使用 `fclose` 函数：

```c
#include <stdio.h>

int main() {
    // 打开文件以写入
    FILE *file = fopen("example.txt", "w");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 向文件写入数据
    fputs("Hello, World!\n", file);

    // 关闭文件
    if (fclose(file) == 0) {
        printf("File closed successfully.\n");
    } else {
        perror("Error closing file");
    }

    // 重新打开文件以读取
    file = fopen("example.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 读取文件内容并输出
    char buffer[100];
    while (fgets(buffer, sizeof(buffer), file) != NULL) {
        printf("%s", buffer);
    }

    // 关闭文件
    if (fclose(file) == 0) {
        printf("File closed successfully.\n");
    } else {
        perror("Error closing file");
    }

    return 0;
}
```

#### 总结

`fclose` 函数是 C 语言中进行文件操作的重要组成部分。通过调用 `fclose`，程序能够确保文件被正确关闭，从而避免潜在的资源泄漏和数据丢失。
