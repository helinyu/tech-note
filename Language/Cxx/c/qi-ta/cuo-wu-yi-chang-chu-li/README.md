# 错误/异常处理



#### 用法

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

void perror(const char *s);
```

* **参数**：`s`是一个指向字符串的指针，用于在错误信息前添加上下文信息。
* **返回值**：没有返回值，直接将错误信息打印到标准错误输出。

#### 示例代码

```c
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main() {
    FILE *file = fopen("non_existent_file.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        // 或者可以打印errno的具体值
        printf("Error number: %d\n", errno);
        return EXIT_FAILURE;
    }
    
    // 文件操作...
    
    fclose(file);
    return EXIT_SUCCESS;
}
```

#### 输出示例

如果文件`non_existent_file.txt`不存在，程序会输出类似如下的信息：

```
Error opening file: No such file or directory
Error number: 2
```

#### 注意事项

* `errno`在每次调用可能设置它的函数后需要检查，因此通常在检测错误后立即使用`perror`。
* `perror`会根据`errno`的值来决定输出哪条错误信息，可能会在不同的系统上返回不同的错误字符串。
* 如果`s`为`NULL`，只会打印错误信息。













