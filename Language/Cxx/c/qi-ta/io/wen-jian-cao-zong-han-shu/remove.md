# remove

在 C 语言中，`remove` 函数用于删除文件。它是由标准库 `<stdio.h>` 提供的。

#### `remove` 函数的原型

```c
int remove(const char *filename);
```

#### 参数

* **`filename`**：指向要删除的文件的路径。

#### 返回值

* 返回 `0` 表示成功。
* 返回一个非零值表示失败，并且可以使用 `errno` 来获取错误代码。

#### 使用注意事项

* `remove` 函数只能删除文件，不能用于删除目录。如果需要删除目录，可以使用 `rmdir` 函数。
* 删除文件时，如果该文件正在被某个程序打开，可能会导致未定义行为。
* 被删除的文件不能被恢复，除非有备份。

#### 示例代码

以下是一个简单的示例，展示如何使用 `remove` 函数：

```c
#include <stdio.h>

int main() {
    const char *filename = "example.txt";

    // 创建一个示例文件
    FILE *file = fopen(filename, "w");
    if (file == NULL) {
        perror("Error creating file");
        return 1;
    }
    fputs("This file will be removed.", file);
    fclose(file);

    // 删除文件
    if (remove(filename) == 0) {
        printf("File '%s' removed successfully.\n", filename);
    } else {
        perror("Error removing file");
    }

    return 0;
}
```

#### 总结

`remove` 函数是一个简单且有效的方法，用于在 C 语言中删除文件。请小心使用，因为删除的文件无法恢复。
