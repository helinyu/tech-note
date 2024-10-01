# 文件

在 C 语言中，文件操作是通过标准库提供的函数来完成的，主要包括打开、关闭、读写文件等。以下是 C 语言中文件的基本概念和常用操作。

#### 1. 文件类型

在 C 语言中，文件通过 `FILE` 类型的指针表示。要处理文件，你需要包含 `<stdio.h>` 头文件。

#### 2. 文件打开和关闭

* **打开文件**：使用 `fopen()` 函数。
* **关闭文件**：使用 `fclose()` 函数。

**示例**：

```c
FILE *file = fopen("example.txt", "r"); // 以只读模式打开文件
if (file == NULL) {
    perror("Error opening file");
    return 1;
}

// 进行文件操作...

fclose(file); // 关闭文件
```

#### 3. 文件模式

在 `fopen()` 函数中，你可以使用不同的模式打开文件：

* `"r"`: 只读模式，文件必须存在。
* `"w"`: 只写模式，文件不存在则创建，存在则清空。
* `"a"`: 追加模式，文件不存在则创建，存在则在文件末尾添加内容。
* `"rb"`, `"wb"`, `"ab"`: 二进制模式的只读、只写和追加模式。

#### 4. 文件读写

* **读文件**：
  * `fgetc()`: 读取一个字符。
  * `fgets()`: 读取一行字符串。
  * `fread()`: 从文件中读取数据块。
* **写文件**：
  * `fputc()`: 写入一个字符。
  * `fputs()`: 写入字符串。
  * `fwrite()`: 向文件写入数据块。

**示例**：

```c
// 读取文件
char ch;
while ((ch = fgetc(file)) != EOF) {
    putchar(ch); // 输出字符到标准输出
}

// 写入文件
FILE *fileWrite = fopen("output.txt", "w");
if (fileWrite != NULL) {
    fputs("Hello, World!", fileWrite);
    fclose(fileWrite);
}
```

#### 5. 文件定位

使用 `fseek()`、`ftell()` 和 `rewind()` 来控制文件指针的位置。

#### 6. 错误处理

使用 `feof()`、`ferror()` 和 `clearerr()` 来处理文件操作中的错误。

