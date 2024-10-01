# 文件定位

C语言中的文件定位函数主要包括：

1. [**`fseek(FILE *stream, long offset, int whence)`**](fseek.md)：
   * 用于移动文件指针到指定的位置。`whence` 可以是 `SEEK_SET`（从文件开头）、`SEEK_CUR`（从当前位置）或 `SEEK_END`（从文件末尾）。
2. [**`ftell(FILE *stream)`**](ftell.md)：
   * 返回当前文件指针的位置，以字节为单位。
3. [**`rewind(FILE *stream)`**](rewind.md)：
   * 将文件指针移动到文件的开头，且清空错误标志。

这些函数可以帮助你在文件中随机访问数据。如果需要更多细节，欢迎询问！
