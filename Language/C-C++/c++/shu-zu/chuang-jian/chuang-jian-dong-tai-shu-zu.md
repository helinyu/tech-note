# 创建动态数组



在 C++中可以使用 `new` 运算符来动态分配数组内存。

```cpp
#include <iostream>

int main() {
    int length = 10;
    int *arr = new int[length];

    // 使用数组
    for (int i = 0; i < length; i++) {
        arr[i] = i;
    }

    // 释放内存
    delete[] arr;
    return 0;
}
```

也可以使用 `std::vector`，它能更方便地进行动态大小调整和内存管理，并且不用担心内存泄漏问题。

```cpp
#include <iostream>
#include <vector>

int main() {
    int length = 10;
    std::vector<int> arr(length);

    // 使用数组
    for (int i = 0; i < length; i++) {
        arr[i] = i;
    }

    return 0;
}
```
