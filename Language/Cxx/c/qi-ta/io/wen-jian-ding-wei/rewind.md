# rewind

`rewind` 函数用于<mark style="color:red;">将文件指针重置到文件的开头</mark>。其原型如下：

```c
void rewind(FILE *stream);
```

#### 参数说明：

* **`stream`**：指向一个 `FILE` 对象的指针，该对象代表要重置的文件。

#### 功能：

* `rewind` 不仅将文件指针移动到文件的起始位置，还会清除与流相关的错误标志。

#### 示例代码：

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 读取一些数据
    char buffer[100];
    fgets(buffer, sizeof(buffer), file);
    printf("Read: %s\n", buffer);

    // 重置文件指针
    rewind(file);

    // 再次读取数据
    fgets(buffer, sizeof(buffer), file);
    printf("Read again: %s\n", buffer);

    fclose(file);
    return 0;
}
```

`rewind` 是快速回到文件开头的便捷方法，适合于重新读取文件的场景。

