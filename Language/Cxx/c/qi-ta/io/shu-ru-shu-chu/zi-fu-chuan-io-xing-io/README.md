# 字符串IO - 行IO

* `char *gets(char *str)`：从标准输入读取一行字符串（不推荐使用）。
* char \*fgets(char \*str, int num, FILE \*stream);  从文件中读取字符串数据
* `int puts(const char *str)`：向标准输出写入字符串。
* &#x20;int fputs(const char \*str, FILE \*stream);  将字符串写入到文件中

&#x20;       2、_<mark style="color:red;">格式化</mark>_输入/输出函数：

* `int scanf(const char *format, ...)`：从标准输入读取格式化数据。
* `int fscanf(FILE *stream, const char *format, ...)`：从指定文件读取格式化数据。
* `int printf(const char *format, ...)`：格式化输出到标准输出。
* `int fprintf(FILE *stream, const char *format, ...)`：格式化输出到指定文件。
