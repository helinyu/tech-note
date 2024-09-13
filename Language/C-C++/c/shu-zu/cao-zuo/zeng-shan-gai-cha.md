# 增删改查

在C语言中，数组是一块固定大小的连续内存区域，数组的大小在声明时就确定了，无法在运行时动态改变。

因此，在C语言中直接对数组进行“增删”操作是比较复杂的，因为数组本身并不支持动态调整大小。

不过，通过使用指针和手动管理内存，我们可以模拟“增删改查”的操作。



#### 1. 数组元素的查询（查）

数组的查询是最简单的操作，直接通过索引访问对应的元素。

**示例：查询数组中的元素**

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int index = 2;
    
    // 查询数组中索引为2的元素
    printf("Element at index %d: %d\n", index, arr[index]);

    return 0;
}
```

#### 2. 修改数组元素（改）

修改数组元素也是相对简单的，只需要通过索引直接访问并重新赋值即可。

**示例：修改数组中的元素**

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int index = 1;
    int newValue = 25;
    
    // 修改索引为1的元素，将其更新为25
    arr[index] = newValue;
    
    // 输出修改后的数组
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    
    return 0;
}
```

#### 3. 插入元素（增）

由于C语言数组是固定大小的，要在数组中插入一个元素，需要将元素后移，并且可能需要重新分配新的内存以扩大数组大小。

**方法1：如果数组大小足够，可以直接移动元素并插入新的元素。**

**示例：在数组中插入元素**

```c
#include <stdio.h>

int main() {
    int arr[6] = {10, 20, 30, 40, 50};  // 数组有6个元素的空间，但只有5个有效元素
    int size = 5;  // 当前数组大小
    int insertIndex = 2;  // 要插入的位置
    int newValue = 25;

    // 将插入位置后的元素右移一位
    for (int i = size; i > insertIndex; i--) {
        arr[i] = arr[i - 1];
    }

    // 插入新元素
    arr[insertIndex] = newValue;
    size++;

    // 输出修改后的数组
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

**方法2：动态分配内存来调整数组大小**

如果数组的大小不够，可以通过`malloc`/`realloc`来动态分配新的数组并插入元素。

**示例：使用`realloc`动态调整数组大小并插入元素**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr = (int *)malloc(5 * sizeof(int));  // 动态分配大小为5的数组
    int size = 5;
    
    // 初始化数组
    for (int i = 0; i < size; i++) {
        arr[i] = (i + 1) * 10;
    }

    int insertIndex = 2;
    int newValue = 25;

    // 动态调整数组大小
    arr = (int *)realloc(arr, (size + 1) * sizeof(int));
    
    // 将插入位置后的元素右移一位
    for (int i = size; i > insertIndex; i--) {
        arr[i] = arr[i - 1];
    }

    // 插入新元素
    arr[insertIndex] = newValue;
    size++;

    // 输出修改后的数组
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }

    // 释放动态分配的内存
    free(arr);

    return 0;
}
```

#### 4. 删除元素（删）

删除数组中的元素，需要将后面的元素向前移动，并减少数组的有效大小。

**示例：删除数组中的元素**

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int size = 5;
    int deleteIndex = 2;

    // 将要删除位置后的元素向左移动
    for (int i = deleteIndex; i < size - 1; i++) {
        arr[i] = arr[i + 1];
    }

    size--;  // 减少数组的有效大小

    // 输出删除后的数组
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

#### 5. 小结

* **查询（查）**：直接通过索引访问元素。
* **修改（改）**：通过索引重新赋值。
* **插入（增）**：需要将插入点后面的元素后移，如果数组大小不足，可以使用动态内存分配`realloc`来扩大数组。
* **删除（删）**：将删除点后的元素前移，减少数组的有效大小。

由于C语言中数组的大小是固定的，在插入或删除元素时可能需要手动管理内存，特别是当数组大小不足时，需要使用动态内存分配函数（如`malloc`和`realloc`）来调整数组的大小。
