# STDIN\_FILENO

`STDIN_FILENO`是一个在 C 和 C++ 中定义的宏，表示标准输入（通常是键盘输入）的文件描述符。

在 Unix-like 系统中，文件描述符是一个小的非负整数，用于标识打开的文件或流。`STDIN_FILENO`的值通常为 0。

以下是一些常见的标准文件描述符宏：

* `STDIN_FILENO`：标准输入。
* `STDOUT_FILENO`：标准输出。
* `STDERR_FILENO`：标准错误输出。

例如，可以使用`read`函数从标准输入读取数据：

```c
#include <unistd.h>
#include <stdio.h>

int main() {
    char buffer[100];
    ssize_t bytesRead = read(STDIN_FILENO, buffer, sizeof(buffer));
    if (bytesRead > 0) {
        buffer[bytesRead] = '\0';
        printf("从标准输入读取到的内容：%s", buffer);
    } else {
        perror("读取错误");
    }
    return 0;
}
```
