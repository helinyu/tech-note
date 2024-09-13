# realloc的使用

在 C 语言中，`realloc`函数用于调整（通常是扩大或缩小）先前通过`malloc`、`calloc`或`realloc`分配的内存块的大小。

以下是`realloc`的函数原型：

```c
void *realloc(void *ptr, size_t size);
```

* `ptr`：是指向要调整大小的内存块的指针。如果这是一个`NULL`指针，`realloc`的行为就像`malloc(size)`，分配一个新的内存块。
* `size`：是新的内存块大小，以字节为单位。

下面是一个使用`realloc`的例子：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)malloc(5 * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    for (int i = 0; i < 5; i++) {
        arr[i] = i;
    }

    // 扩大数组大小到 10 个元素
    int *newArr = (int *)realloc(arr, 10 * sizeof(int));
    if (newArr == NULL) {
        printf("Memory reallocation failed.\n");
        free(arr);
        return 1;
    }

    // 使用新的扩大后的数组
    for (int i = 5; i < 10; i++) {
        newArr[i] = i;
    }

    // 释放内存
    free(newArr);

    return 0;
}
```

在使用`realloc`时需要注意以下几点：

1. 如果内存扩大成功，`realloc`返回一个指向新分配内存的指针，这个指针可能与原来的指针不同，所以在使用`realloc`后，应该使用新的指针来访问内存块。
2. 如果内存扩大失败，`realloc`返回`NULL`，同时原来的内存块不会被改变，仍然有效。在这种情况下，应该根据需要决定是否释放原来的内存块。
3. 如果`realloc`的第一个参数是`NULL`，它的行为就像`malloc`，分配一个新的内存块。
4. 尽量避免频繁地使用`realloc`来扩大内存，因为这可能导致内存碎片和性能问题。如果预先知道需要的内存大小，可以一次性分配足够的内存。

## 小结

1、尽量不要使用

2、是在原来数组的内存空间扩展内存的
