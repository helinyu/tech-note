# fread

`fread` 是 C 语言中用于<mark style="color:red;">从文件中读取二进制数据的函数</mark>。以下是它的主要信息：

#### 函数原型

```c
size_t fread(void *ptr, size_t size, size_t count, FILE *stream);
```

#### 参数

* **`ptr`**：指向存储读取数据的内存块的指针。
* **`size`**：每个元素的字节大小。
* **`count`**：要读取的元素数量。
* **`stream`**：指向要读取的文件流的 `FILE` 指针。

#### 返回值

* 返回实际读取的元素数量。如果返回值小于 `count`，可能是因为到达文件末尾或发生错误。

#### 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp;
    int numbers[5];

    // 打开文件进行读取
    fp = fopen("numbers.bin", "rb");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 读取二进制数据
    size_t result = fread(numbers, sizeof(int), 5, fp);
    if (result != 5) {
        if (feof(fp)) {
            printf("到达文件末尾。\n");
        } else {
            perror("读取错误");
        }
    }

    fclose(fp);

    // 输出读取的数据
    for (size_t i = 0; i < result; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    return 0;
}
```

#### 注意事项

* 确保提供的缓冲区（`ptr`）有足够的内存来存储读取的数据。
* 在读取后，检查返回值以确认实际读取的元素数量。
* 如果需要处理文本数据，考虑使用 `fgets` 或 `fscanf` 等函数。

