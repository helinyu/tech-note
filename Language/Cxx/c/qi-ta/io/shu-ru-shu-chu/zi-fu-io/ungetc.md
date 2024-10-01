# ungetc

`ungetc` 是 C 语言中的一个函数，用于将一个字符放回到文件流中，使下次读取时可以再次读取到这个字符。以下是 `ungetc` 的主要信息：

#### 函数原型

```c
int ungetc(int c, FILE *stream);
```

#### 参数

* **`c`**：要放回的字符，以 `int` 类型表示。
* **`stream`**：指向一个 `FILE` 对象的指针，表示要操作的文件流。

#### 返回值

* 成功时返回放回的字符（通常是 `c`），失败时返回 `EOF`。

#### 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("example.txt", "r");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    int c = fgetc(fp); // 读取一个字符
    if (c != EOF) {
        printf("读取的字符: %c\n", c);
        ungetc(c, fp); // 将字符放回流中
    }

    int d = fgetc(fp); // 再次读取
    if (d != EOF) {
        printf("再次读取的字符: %c\n", d); // 应该是之前读取的字符
    }

    fclose(fp);
    return 0;
}
```

#### 注意事项

* `ungetc` 只能放回一个字符，不能放回多个字符。
* 只能在当前读取流中使用，放回字符的流必须与读取字符的流相同。
* 不能将 `EOF` 作为参数传递给 `ungetc`。

