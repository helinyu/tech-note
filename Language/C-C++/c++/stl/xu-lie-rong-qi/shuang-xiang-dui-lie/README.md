---
description: std::deque
---

# 双向队列

`std::deque`（双端队列，double-ended queue）是 C++ 标准模板库（STL）中的一种序列容器。`std::deque` 允许在序列的两端高效地插入和删除元素，既可以在头部操作，也可以在尾部操作。

#### 1. **`std::deque` 的主要特点**

* **双端操作**：支持在头部和尾部都能进行高效的插入和删除操作，插入和删除的时间复杂度为 O(1)。
* **随机访问**：`std::deque` 支持常数时间的随机访问，类似于 `std::vector`，可以通过下标访问任意位置的元素。
* **灵活的内存管理**：与 `std::vector` 不同，`std::deque` 的内存管理不是连续的。它使用一系列的固定大小的块来存储数据，因此不需要像 `std::vector` 那样在内存不足时重新分配整个内存。
* **常见操作的效率**：
  * 头尾插入/删除：O(1)
  * 随机访问：O(1)
  * 插入/删除（中间）：O(n)

#### 2. **`std::deque` 的常用方法**

**2.1 插入元素**

*   **`push_back(const T& value)`**：在尾部插入元素 `value`。

    ```cpp
    std::deque<int> d;
    d.push_back(10);  // 在尾部插入 10
    d.push_back(20);  // 在尾部插入 20
    ```
*   **`push_front(const T& value)`**：在头部插入元素 `value`。

    ```cpp
    d.push_front(5);  // 在头部插入 5
    ```
*   **`insert(iterator position, const T& value)`**：在迭代器 `position` 所指向的位置之前插入元素 `value`。

    ```cpp
    auto it = d.begin();
    d.insert(it, 15);  // 在开头插入 15
    ```
*   **`emplace_back(Args&&... args)`**：在尾部原位构造元素。

    ```cpp
    d.emplace_back(30);  // 在尾部原位构造 30
    ```
*   **`emplace_front(Args&&... args)`**：在头部原位构造元素。

    ```cpp
    d.emplace_front(1);  // 在头部原位构造 1
    ```

**2.2 删除元素**

*   **`pop_back()`**：移除尾部的元素。

    ```cpp
    d.pop_back();  // 移除尾部元素
    ```
*   **`pop_front()`**：移除头部的元素。

    ```cpp
    d.pop_front();  // 移除头部元素
    ```
*   **`erase(iterator position)`**：删除迭代器 `position` 所指向的元素。

    ```cpp
    d.erase(d.begin());  // 删除第一个元素
    ```
*   **`clear()`**：删除容器中的所有元素。

    ```cpp
    d.clear();  // 清空 deque
    ```

**2.3 访问元素**

*   **`operator[]`**：通过下标随机访问元素。

    ```cpp
    int elem = d[0];  // 访问第一个元素
    ```
*   **`at(size_type n)`**：通过下标访问元素，超出范围会抛出异常。

    ```cpp
    int elem = d.at(1);  // 访问第二个元素
    ```
*   **`front()`**：返回头部的元素。

    ```cpp
    int firstElem = d.front();
    ```
*   **`back()`**：返回尾部的元素。

    ```cpp
    int lastElem = d.back();
    ```

**2.4 遍历元素**

*   **使用迭代器遍历**：

    ```cpp
    for (auto it = d.begin(); it != d.end(); ++it) {
        std::cout << *it << " ";
    }
    ```
*   **使用范围循环遍历**：

    ```cpp
    for (int elem : d) {
        std::cout << elem << " ";
    }
    ```

**2.5 其他操作**

*   **`size()`**：返回 deque 中的元素数量。

    ```cpp
    std::cout << "Size: " << d.size() << std::endl;
    ```
*   **`empty()`**：检查 deque 是否为空。如果 deque 为空，则返回 `true`。

    ```cpp
    if (d.empty()) {
        std::cout << "Deque is empty" << std::endl;
    }
    ```
*   **`resize(size_type n)`**：调整 deque 的大小。如果当前大小小于 `n`，则插入默认值填充；如果大于 `n`，则移除多余的元素。

    ```cpp
    d.resize(5);
    ```

#### 3. **示例代码**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> d = {10, 20, 30};

    // 插入元素
    d.push_front(5);  // 在头部插入
    d.push_back(40);  // 在尾部插入

    // 遍历 deque
    for (const auto& elem : d) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 访问元素
    std::cout << "Front: " << d.front() << std::endl;
    std::cout << "Back: " << d.back() << std::endl;

    // 删除元素
    d.pop_front();  // 删除头部元素
    d.pop_back();   // 删除尾部元素

    // 通过下标访问
    std::cout << "Element at index 1: " << d[1] << std::endl;

    return 0;
}
```

#### 4. **`std::deque` 的常见应用场景**

**1. 需要频繁的双端操作**

当程序中需要在序列的头部和尾部频繁进行插入和删除操作时，`std::deque` 提供了比 `std::vector` 更高效的操作方式。`std::deque` 可以 O(1) 时间复杂度进行双端插入和删除，而 `std::vector` 在头部插入或删除时则需要移动所有元素。

**2. 任务调度或滑动窗口问题**

`std::deque` 常用于实现任务调度系统，或是解决滑动窗口类的问题。由于可以在双端高效操作，因此它适合管理动态更新的序列数据。

**3. 需要高效的随机访问**

尽管 `std::deque` 在插入/删除方面的表现比 `std::vector` 更好，但它仍支持高效的随机访问，这使它在需要在头尾频繁插入元素，同时还要随机访问某些数据的场景下非常有用。

#### 5. **总结**

| 操作             | 描述          |
| -------------- | ----------- |
| `push_back()`  | 在尾部插入元素     |
| `push_front()` | 在头部插入元素     |
| `pop_back()`   | 删除尾部的元素     |
| `pop_front()`  | 删除头部的元素     |
| `operator[]`   | 随机访问元素      |
| `at()`         | 安全地访问元素     |
| `front()`      | 返回头部元素      |
| `back()`       | 返回尾部元素      |
| `insert()`     | 在指定位置插入元素   |
| `erase()`      | 删除指定位置的元素   |
| `size()`       | 返回元素个数      |
| `empty()`      | 检查是否为空      |
| `resize()`     | 调整 deque 大小 |

`std::deque` 是一种灵活的容器，适合在需要双端操作和随机访问的场景下使用，能够比 `std::vector` 提供更好的性能，尤其是在需要频繁修改头部的情况下。
