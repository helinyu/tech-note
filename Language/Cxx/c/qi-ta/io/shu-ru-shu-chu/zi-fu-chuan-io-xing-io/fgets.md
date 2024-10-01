# fget函数

`fgets`函数用于从文件流中读取一行文本。以下是关于它的详细信息：

#### 1. **语法**

```c
char *fgets(char *str, int num, FILE *stream);
```

#### 2. **参数**

* `str`：指向存储读取行的字符数组的指针。
* `num`：要读取的最大字符数（包括结束的空字符）。
* `stream`：指向输入文件流的指针，通常是`stdin`或其他打开的文件指针。

#### 3. **返回值**

* 成功时返回指向`str`的指针，失败时返回`NULL`。读取结束的条件包括到达文件末尾或发生错误。

#### 4. **使用场景**

* **读取用户输入**：可以从标准输入读取用户输入的行。
* **处理文件内容**：可用于逐行读取文件内容，适合处理文本文件。

#### 5. **注意事项**

* `fgets`会包括行末的换行符（如果有），但会在字符数组末尾添加空字符。
* 需要确保提供的字符数组足够大以存储读取的内容及结束符，以避免缓冲区溢出。

#### 示例代码

```c
#include <stdio.h>

int main() {
    char buffer[100]; // 存储读取的行

    printf("Enter a line of text: ");
    if (fgets(buffer, sizeof(buffer), stdin) != NULL) {
        printf("You entered: %s", buffer);
    } else {
        printf("Error reading input.\n");
    }

    return 0;
}
```

在这个示例中，`fgets`从标准输入读取一行文本，并将其存储在`buffer`中。然后输出用户输入的内容。



—— 要看一下C语言中的输入输出的内容了， 以前都没看过，尴尬了
