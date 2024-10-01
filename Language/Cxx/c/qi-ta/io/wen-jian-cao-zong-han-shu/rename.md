# rename

在 C 语言中，`rename` 函数用于重命名一个文件或目录。它是由标准库 `<stdio.h>` 提供的。

#### `rename` 函数的原型

```c
int rename(const char *oldname, const char *newname);
```

#### 参数

* **`oldname`**：指向要重命名的现有文件或目录的路径。
* **`newname`**：指向新的文件名或路径的字符串。

#### 返回值

* 返回 `0` 表示成功。
* 返回一个非零值表示失败，并且可以使用 `errno` 来获取错误代码。

#### 使用注意事项

* 如果目标文件（`newname`）已经存在，`rename` 会失败，除非你在不同的文件系统上进行重命名操作。
* `rename` 不会复制文件内容，只是更改文件的名称或位置。
* 如果重命名的文件正在被打开，则可能会导致未定义行为。

#### 示例代码

以下是一个简单的示例，展示如何使用 `rename` 函数：

```c
#include <stdio.h>

int main() {
    const char *oldFilename = "old_file.txt";
    const char *newFilename = "new_file.txt";

    // 创建一个示例文件
    FILE *file = fopen(oldFilename, "w");
    if (file == NULL) {
        perror("Error creating file");
        return 1;
    }
    fputs("This is an old file.", file);
    fclose(file);

    // 重命名文件
    if (rename(oldFilename, newFilename) == 0) {
        printf("File renamed successfully from %s to %s\n", oldFilename, newFilename);
    } else {
        perror("Error renaming file");
    }

    return 0;
}
```

#### 结论

`rename` 函数是一个简单且有效的工具，用于在 C 语言中更改文件或目录的名称。
