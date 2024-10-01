# exit

`exit`函数用于终止程序并返回状态码。它的基本定义如下：

#### 定义

```c
#include <stdlib.h>

void exit(int status);

#define	EXIT_FAILURE	1 // 错误退出
#define	EXIT_SUCCESS	0 // 成功退出

```

* **参数**：`status`是一个整数，通常用于指示程序的退出状态。`0`表示成功，非零值表示错误。



#### 使用示例

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("Program is running...\n");

    // 根据某个条件决定是否退出
    if (_condition) {
        printf("An error occurred!\n");
        exit(1); // 以错误状态退出
    }

    printf("Program completed successfully.\n");
    exit(0); // 正常退出
}
```

#### 注意事项

* `exit`会执行所有已注册的[`atexit`](atexit.md)函数，并刷新输出缓冲区。
* 在多线程程序中，`exit`会终止调用它的线程并关闭程序。

