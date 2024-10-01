# fwrite

`fwrite` 是 C 语言中用于<mark style="color:red;">将二进制数据写入文件的函数</mark>。以下是它的主要信息：

#### 函数原型

```c
size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
```

#### 参数

* **`ptr`**：指向要写入的内存块的指针。
* **`size`**：每个元素的字节大小。
* **`count`**：要写入的元素数量。
* **`stream`**：指向要写入的文件流的 `FILE` 指针。

#### 返回值

* 返回实际写入的元素数量。如果返回值小于 `count`，可能是因为发生错误。

#### 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp;
    int numbers[] = {1, 2, 3, 4, 5};

    // 打开文件进行写入
    fp = fopen("numbers.bin", "wb");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 写入二进制数据
    size_t result = fwrite(numbers, sizeof(int), 5, fp);
    if (result != 5) {
        perror("写入错误");
    }

    fclose(fp);
    return 0;
}
```

#### 注意事项

* 确保文件以二进制模式（`wb`）打开，以正确写入二进制数据。
* 提供的内存块（`ptr`）必须有效且包含要写入的数据。
* 检查返回值以确认实际写入的元素数量，确保没有发生错误。

