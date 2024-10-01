# 二进制IO

* [`size_t fread(void *ptr, size_t size, size_t count, FILE *stream)`：从文件中读取数据。](fread.md)
* [`size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream)`：向文件写入数据](fwrite.md)。

{% code title="示例代码" %}
```
#include <stdio.h>

int main() {
    FILE *fp;
    int numbers[] = {1, 2, 3, 4, 5};
    int read_numbers[5];

    // 写入二进制文件
    fp = fopen("numbers.bin", "wb");
    if (fp == NULL) {
        perror("Error opening file for writing");
        return 1;
    }
    fwrite(numbers, sizeof(int), 5, fp);
    fclose(fp);

    // 读取二进制文件
    fp = fopen("numbers.bin", "rb");
    if (fp == NULL) {
        perror("Error opening file for reading");
        return 1;
    }
    fread(read_numbers, sizeof(int), 5, fp);
    fclose(fp);

    // 输出读取的数据
    for (int i = 0; i < 5; i++) {
        printf("%d ", read_numbers[i]);
    }
    printf("\n");

    return 0;
}

```
{% endcode %}

#### 注意事项

* 在使用 `fread` 和 `fwrite` 时，要确保传入的指针有效且具有足够的内存。
* 二进制文件不可以用文本编辑器打开，通常是不可读的。
