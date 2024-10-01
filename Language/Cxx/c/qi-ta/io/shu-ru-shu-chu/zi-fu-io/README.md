# 字符IO



### 1、 输入

* `int getc(FILE *stream)`：从<mark style="color:red;">文件</mark>中读取一个字符。 <mark style="color:orange;">宏定义 （优选）</mark>
* `int fgetc(FILE *stream)`：从<mark style="color:red;">文件</mark>中读取一个字符。 <mark style="color:orange;">函数</mark>
* `int getchar(void)`：从<mark style="color:red;">标准</mark>输入读取一个字符。



### 2、输出

* `int putc(int char, FILE *stream)`：向<mark style="color:red;">文件</mark>写入一个字符。 <mark style="color:orange;">宏定义（优选）</mark>
* `int fputc(int char, FILE *stream)`：向<mark style="color:red;">文件</mark>写入一个字符。 <mark style="color:orange;">函数</mark>
* `int putchar(int char)`：向<mark style="color:red;">标准</mark>输出写入一个字符。



### 3、撤销字符IO

* int ungetc(int c, FILE \*stream);  将一个字符放回到文件流中，使下次读取时可以再次读取到这个字符。

