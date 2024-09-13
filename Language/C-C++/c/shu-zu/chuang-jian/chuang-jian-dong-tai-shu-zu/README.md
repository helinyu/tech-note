# 创建动态数组

以下是在 C 中动态生成指定长度数组的方法， 这个长度是一个变量。

**一、C 语言**

在 C 语言中可以使用 `malloc`、`calloc` 或 `realloc` 函数从堆上动态分配内存来创建一个指定长度的数组。

1. 使用 `malloc`：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int length = 10;
    int *arr = (int *)malloc(length * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // 使用数组
    for (int i = 0; i < length; i++) {
        arr[i] = i;
    }

    // 释放内存
    free(arr);
    return 0;
}
```

2. 使用 `calloc`： `calloc` 与 `malloc` 的主要区别在于 `calloc` 会将分配的内存初始化为 0。

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int length = 10;
    int *arr = (int *)calloc(length, sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // 使用数组，此时数组元素已经初始化为 0

    // 释放内存
    free(arr);
    return 0;
}
```

