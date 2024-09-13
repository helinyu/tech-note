# 迭代器

常见的迭代器next和while的结合，

其实迭代器就类似我们常见的i ,通过i++访问数组一样，不同的数据结构可能迭代器还不一样。

以下是一个在 C++中使用迭代器结合 `while` 循环遍历容器的例子：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 使用迭代器和 while 循环遍历 vector
    auto it = vec.begin();
    while (it!= vec.end()) {
        std::cout << *it << " ";
        it++;
    }
    std::cout << std::endl;

    return 0;
}
```

在这个例子中，通过迭代器 `it` 从容器的开头开始遍历，在 `while` 循环中不断检查是否到达容器末尾，如果没有到达末尾就输出当前元素并将迭代器向前移动一步（`it++`）。

你还可以使用 `while` 循环结合双向迭代器进行双向遍历，或者使用随机访问迭代器进行更复杂的遍历操作。例如：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 双向遍历
    auto it = vec.end();
    while (it!= vec.begin()) {
        --it;
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 随机访问迭代器的 while 循环遍历
    it = vec.begin();
    while (it < vec.end()) {
        std::cout << *it << " ";
        it += 2; // 每次移动两步
    }
    std::cout << std::endl;

    return 0;
}
```

C++中不同的容器的迭代器可能还不一样。
