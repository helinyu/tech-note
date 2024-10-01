# fseek

`fseek` 函数用于设置文件流的当前位置。其原型如下：

```c
int fseek(FILE *stream, long offset, int whence);
```

#### 参数说明：

* **`stream`**：指向一个 `FILE` 对象的指针，该对象代表要操作的文件。
* **`offset`**：要移动的字节数。可以是正值或负值。
* **`whence`**：指定起始位置的标志，取值如下：
  * `SEEK_SET`：从文件开头开始偏移。
  * `SEEK_CUR`：从当前位置开始偏移。
  * `SEEK_END`：从文件末尾开始偏移。

#### 返回值：

* 成功时返回 `0`，失败时返回 `-1`。

#### 示例代码：

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // 移动到文件的第10个字节
    if (fseek(file, 10, SEEK_SET) != 0) {
        perror("Error seeking");
        fclose(file);
        return 1;
    }

    // 读取和处理数据...

    fclose(file);
    return 0;
}
```

使用 `fseek` 可以实现随机访问文件中的数据，适合需要频繁跳转读取的场景。

