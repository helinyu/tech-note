---
description: for
---

# for

### 1、传统`for` 循环&#x20;

```c
for (初始化语句; 循环条件; 更新语句) {
    // 循环体
}
```

和C语言是一样的



### 2、使用范围 `for` 循环（C++11 及以上）：

```
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    for (int value : vec) {
        std::cout << value << " ";
    }
    std::cout << std::endl;
    return 0;
}
```
