# 流错误函数

C语言中用于处理文件流错误的函数主要有以下几个：

1. **`clearerr(FILE *stream)`**：
   * 清除文件流的错误标志，使其可以重新进行读写操作。
2. **`feof(FILE *stream)`**：
   * 检查是否已到达文件末尾。返回非零值表示到达末尾，零表示未到达。
3. **`ferror(FILE *stream)`**：
   * 检查文件流是否发生错误。返回非零值表示有错误，零表示没有错误。

#### 示例代码：

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 尝试读取
    char buffer[100];
    if (fgets(buffer, sizeof(buffer), file) == NULL) {
        if (ferror(file)) {
            perror("Error reading from file");
        } else if (feof(file)) {
            printf("Reached end of file\n");
        }
    }

    clearerr(file); // 清除错误标志

    fclose(file);
    return 0;
}
```

这些函数可以帮助你<mark style="color:red;">检测和处理文件流中的错误</mark>。
