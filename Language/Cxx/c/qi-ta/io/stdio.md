# stdio

`stdio.h` 中的函数主要可以分为以下几类：

1. **标准输入输出函数**：
   * `printf()`: 格式化输出到标准输出。
   * `scanf()`: 格式化输入从标准输入。
2. **字符输入输出函数（标准）**：
   * `getchar()`: 从标准输入读取一个字符。
   * `putchar()`: 将一个字符写入标准输出。
3. **字符串输入输出函数（标准）**：
   * `gets()`: 读取一行字符串（不推荐使用）。
   * `puts()`: 输出字符串并换行。
4. **文件操作函数**：
   * `fopen()`: 打开文件。
   * `fclose()`: 关闭文件。
   * `fread()`, `fwrite()`: 读写文件。
   * `fgets()`, `fputs()`: 读取和写入字符串。
   * fgetc(), fputc()： 读取和写入字符
   * 操作：文件+字符串 、 文件+字符&#x20;



***

1. [**文件定位函数**：](wen-jian-ding-wei/)
   * `fseek()`: 设置文件流的位置。
   * `ftell()`: 返回当前文件位置。
   * `rewind()`: 重置文件位置到开头。
2. **缓冲控制函数**：
   * `setbuf()`, `setvbuf()`: 设置流的缓冲区。
3. **刷新**：
   * [`fflush()`](shua-xin-fflush.md) 清空输出缓冲区，将缓冲区中的数据强制写入到目标文件或设备
4. 。。。

