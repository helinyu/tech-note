# tmpfile & tmpnam

在 C 语言中，临时文件是一种在程序运行期间创建并使用的文件，通常用于存储中间数据或临时信息。临时文件的特点是它们在程序结束时会被自动删除。以下是有关 C 中临时文件的一些重要内容：

#### 1. 创建临时文件

C 标准库提供了 <mark style="color:orange;">`tmpfile()`</mark> <mark style="color:orange;"></mark><mark style="color:orange;">函数，用于创建临时文件</mark>。这个函数会返回一个指向新创建的 `FILE` 对象的指针，该文件在程序结束时会被自动删除。

**`tmpfile()` 函数原型**

```c
FILE *tmpfile(void);
```

#### 2. 使用 `tmpfile()`

当你调用 `tmpfile()` 时，它会创建一个临时文件并返回一个 `FILE` 指针，可以通过该指针进行读写操作。

#### 3. 示例代码

下面是一个使用 `tmpfile()` 创建临时文件的示例：

```c
#include <stdio.h>

int main() {
    // 创建临时文件
    FILE *tempFile = tmpfile();
    if (tempFile == NULL) {
        perror("Error creating temporary file");
        return 1;
    }

    // 向临时文件写入数据
    fputs("This is a temporary file.\n", tempFile);

    // 重置文件指针到开头
    rewind(tempFile);

    // 从临时文件读取数据并输出
    char buffer[100];
    while (fgets(buffer, sizeof(buffer), tempFile) != NULL) {
        printf("%s", buffer);
    }

    // 关闭临时文件（虽然会在程序结束时自动删除）
    fclose(tempFile);

    return 0;
}
```

#### 4. 注意事项

* **自动删除**：临时文件在关闭或程序结束时会被删除，因此不需要手动删除。
* **权限**：临时文件的权限由系统决定，通常对创建它的进程可读写。
* **存储位置**：临时文件的存储位置通常在操作系统的临时目录中，可以通过环境变量（如 `TMP` 或 `TEMP`）来配置。

#### 5. 其他方法

除了使用 `tmpfile()`，还可以使<mark style="color:orange;">用</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`tmpnam()`</mark> <mark style="color:orange;"></mark><mark style="color:orange;">函数获取临时文件名，然后手动创建文件</mark>。不过，使用 `tmpfile()` 更为安全，因为它确保文件不会被其他进程使用。

#### 示例代码（使用 `tmpnam()`）

```c
#include <stdio.h>

int main() {
    char tempFilename[L_tmpnam]; // 临时文件名
    tmpnam(tempFilename); // 获取临时文件名

    // 创建并打开临时文件
    FILE *tempFile = fopen(tempFilename, "w+");
    if (tempFile == NULL) {
        perror("Error creating temporary file");
        return 1;
    }

    // 向临时文件写入数据
    fputs("This is another temporary file.\n", tempFile);

    // 关闭临时文件
    fclose(tempFile);

    return 0;
}
```

#### 总结

临时文件在 C 语言中是一个方便的工具，适用于需要存储中间数据的情况。通过使用 `tmpfile()` 函数，可以轻松创建和使用这些临时文件。

