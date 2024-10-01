# ftell

`ftell` 函数用于<mark style="color:red;">获取当前文件指针的位置</mark>。其原型如下：

```c
long ftell(FILE *stream);
```

#### 参数说明：

* **`stream`**：指向一个 `FILE` 对象的指针，该对象代表要查询的文件。

#### 返回值：

* 返回当前位置的偏移量（以字节为单位）。如果出错，返回 `-1`。

#### 示例代码：

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 移动到文件的第10个字节
    fseek(file, 10, SEEK_SET);

    // 获取当前文件指针位置
    long pos = ftell(file);
    if (pos == -1) {
        perror("Error telling position");
    } else {
        printf("Current position: %ld\n", pos);
    }

    fclose(file);
    return 0;
}
```

`ftell` 函数非常有用，尤其是在<mark style="color:red;">需要跟踪文件读取位置的情况</mark>下。

