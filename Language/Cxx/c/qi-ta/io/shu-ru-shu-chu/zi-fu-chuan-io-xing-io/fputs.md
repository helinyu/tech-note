# fputs

`fputs` 是 C 语言中的一个函数，<mark style="color:red;">**用于将字符串写入指定的文件流**</mark>。以下是它的主要信息：

#### 函数原型

```c
int fputs(const char *str, FILE *stream);
```

#### 参数

* **`str`**：要写入的字符串，必须以空字符 `\0` 结尾。
* **`stream`**：指向一个 `FILE` 对象的指针，表示要写入的文件流。

#### 返回值

* 成功时返回一个非负值（通常是 0），失败时返回 `EOF`。

#### 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("output.txt", "w");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 写入字符串
    fputs("Hello, World!\n", fp);
    fputs("This is a test.\n", fp);

    fclose(fp);
    return 0;
}
```

#### 注意事项

* `fputs` 不会自动添加换行符，如果需要在字符串末尾添加换行符，需要手动加上。
* 使用 `fputs` 写入的字符串必须是以 `\0` 结尾的有效字符串。
* 在写入后，建议使用 `fflush` 来确保数据及时写入文件（如果是以非缓冲模式打开的文件）。

