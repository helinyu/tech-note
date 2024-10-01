# setvbuf函数

`setvbuf()`函数用于控制流（通常是文件流）的缓冲方式。

**函数原型**：

```c
int setvbuf(FILE *stream, char *buf, int mode, size_t size);
```

**参数解释**：

* `stream`：指向要控制缓冲的文件流的指针。
* `buf`：指向用户提供的用于缓冲的存储区域的指针。如果为`NULL`，则由函数自动分配缓冲区。
* `mode`：缓冲模式，有以下几种取值：
  * `_IOFBF`：全缓冲。在缓冲区填满或进行明确的刷新操作之前，数据不会被写入文件。
  * `_IOLBF`：行缓冲。当遇到换行符或缓冲区填满时，数据被写入文件。
  * `_IONBF`：无缓冲。数据会立即被写入文件，不进行缓冲。
* `size`：指定缓冲区的大小（以字节为单位）。仅在`buf`为`NULL`（即自动分配缓冲区）时有效。

**返回值**：

* 如果成功，返回 0。
* 如果失败，返回非零值。

**示例用法**：

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("test.txt", "w");
    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 设置文件流为无缓冲模式
    if (setvbuf(fp, NULL, _IONBF, 0)!= 0) {
        perror("Error setting buffer mode");
        fclose(fp);
        return 1;
    }

    fprintf(fp, "Hello, world!");
    fclose(fp);

    return 0;
}
```

在这个例子中，打开一个文件并将其设置为无缓冲模式，然后向文件中写入内容。由于是无缓冲模式，写入的内容会立即被写入文件，而不是等到缓冲区填满或进行刷新操作。
