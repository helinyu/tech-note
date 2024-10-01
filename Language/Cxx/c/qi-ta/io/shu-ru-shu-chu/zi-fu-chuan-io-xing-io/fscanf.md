# fscanf

`fscanf` 是 C 语言中的一个函数，用于从文件中读取格式化的数据。以下是它的主要信息：

#### 函数原型

```c
int fscanf(FILE *stream, const char *format, ...);
```

#### 参数

* **`stream`**：指向要读取的文件流的 `FILE` 指针。
* **`format`**：格式字符串，指定输入数据的类型和格式。
* **`...`**：指向要存储读取值的变量的指针，数量和类型应与格式字符串匹配。

#### 返回值

* 返回成功读取的项数。如果到达文件末尾或发生错误，返回 `EOF`。

#### 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("data.txt", "r");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    int a;
    float b;
    char str[100];

    // 从文件中读取数据
    int items = fscanf(fp, "%d %f %s", &a, &b, str);

    if (items == 3) {
        printf("读取的整数是: %d\n", a);
        printf("读取的浮点数是: %.2f\n", b);
        printf("读取的字符串是: %s\n", str);
    } else {
        printf("读取错误。\n");
    }

    fclose(fp);
    return 0;
}
```

#### 注意事项

* `fscanf` 与 `scanf` 类似，但用于从文件中读取数据。
* 在使用 `%s` 时，字符串读取会在空格处停止，确保目标数组足够大以避免缓冲区溢出。
* 确保在读取后检查返回值，以确认数据是否正确读取。

