# 输入输出

ANSI C 的一个主要的优点： <mark style="color:orange;">这些修改将通过增加不同函数的方式实现，而不是通过对现存函数进行修改实现， 因此， 程序的可移植性不受影响。</mark>



C语言的标准I/O函数库提供了一组用于输入和输出操作的函数，主要通过以下头文件进行声明：

```c
#include <stdio.h>
```



<figure><img src="../../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 常见的标准I/O函数

1. <mark style="color:red;">**文件操作**</mark>**函数**： （打开、关系）
   * `FILE *fopen(const char *filename, const char *mode)`：打开文件。
   * `int fclose(FILE *stream)`：关闭文件。
2. [<mark style="color:red;">**二进制**</mark>**输入/输出函数**](er-jin-zhi-io/)
   * `size_t fread(void *ptr, size_t size, size_t count, FILE *stream)`：从文件中读取数据。
   * `size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream)`：向文件写入数据。
3. [<mark style="color:red;">**字符**</mark>**输入/输出函数**：](zi-fu-io/)
   * `int getc(FILE *stream)`：从文件中读取一个字符。 宏定义
   * `int fgetc(FILE *stream)`：从文件中读取一个字符。 函数
   * `int getchar(void)`：从标准输入读取一个字符。
   * \-——上面输入、下面输出，对应关系————————
   * `int putc(int char, FILE *stream)`：向文件写入一个字符。 宏定义
   * `int fputc(int char, FILE *stream)`：向文件写入一个字符。 函数
   * `int putchar(int char)`：向标准输出写入一个字符。
4. [<mark style="color:red;">**字符串**</mark>**输入/输出函数 —— 行I/O**：](zi-fu-chuan-io-xing-io/)

&#x20;       1、<mark style="color:red;">未</mark>_<mark style="color:red;">格式化</mark>输入/输出函数：_

* `char *gets(char *str)`：从**标准**输入读取一行字符串（不推荐使用）。
* char \*fgets(char \*str, int num, FILE \*stream);  从**文件**中读取字符串数据
* `int puts(const char *str)`：向标准输出写入字符串。
* &#x20;int fputs(const char \*str, FILE \*stream);  将字符串写入到文件中

&#x20;       2、_<mark style="color:red;">格式化</mark>_输入/输出函数：

* `int scanf(const char *format, ...)`：从标准输入读取格式化数据。
* `int fscanf(FILE *stream, const char *format, ...)`：从指定文件读取格式化数据。
* `int printf(const char *format, ...)`：格式化输出到标准输出。
* `int fprintf(FILE *stream, const char *format, ...)`：格式化输出到指定文件。



#### 注意事项

* 使用`fopen`打开的文件必须使用`fclose`关闭，以避免资源泄漏。
* 在读取和写入数据时，确保正确处理返回值以检测错误。



