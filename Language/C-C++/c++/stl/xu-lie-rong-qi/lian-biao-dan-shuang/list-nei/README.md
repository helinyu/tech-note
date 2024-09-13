# list内

`std::list` 是 C++ 标准模板库（STL）中的一个双向链表容器。它是一种序列式容器，支持高效的插入和删除操作，特别是在非连续存储的情况下。

#### 1. **`std::list` 的主要特点**

* **双向链表**：`std::list` 是一个双向链表，链表中的每个元素都包含指向前一个和后一个元素的指针。这样可以使得在链表中间插入或删除元素的操作非常高效（O(1) 时间复杂度）。
* **随机访问慢**：由于链表不支持随机访问，不能通过下标直接访问元素，因此与 `std::vector` 相比，访问链表中的元素效率较低（O(n) 时间复杂度）。
* **适用于频繁插入/删除的场景**：当应用程序频繁需要在序列中间进行插入或删除操作时，`std::list` 是一个很好的选择。

#### 2. **`std::list` 的常用方法**

**2.1 插入元素**

*   **`push_back(const T& value)`**：在链表的尾部插入元素 `value`。

    ```cpp
    std::list<int> myList;
    myList.push_back(10);  // 在尾部插入 10
    myList.push_back(20);  // 在尾部插入 20
    ```
*   **`push_front(const T& value)`**：在链表的头部插入元素 `value`。

    ```cpp
    myList.push_front(5);  // 在头部插入 5
    ```
*   **`insert(iterator position, const T& value)`**：在迭代器 `position` 所指向的位置之前插入元素 `value`。

    ```cpp
    auto it = myList.begin();
    std::advance(it, 1);  // 将迭代器移动到第二个元素的位置
    myList.insert(it, 15);  // 在第二个元素之前插入 15
    ```
*   **`emplace(iterator position, Args&&... args)`**：在迭代器 `position` 所指向的位置原位构造元素。

    ```cpp
    myList.emplace(myList.begin(), 100);  // 在头部插入 100
    ```

**2.2 删除元素**

*   **`pop_back()`**：移除链表尾部的元素。

    ```cpp
    myList.pop_back();  // 删除尾部元素
    ```
*   **`pop_front()`**：移除链表头部的元素。

    ```cpp
    myList.pop_front();  // 删除头部元素
    ```
*   **`erase(iterator position)`**：删除迭代器 `position` 所指向的元素。

    ```cpp
    auto it = myList.begin();
    std::advance(it, 1);  // 将迭代器移动到第二个元素
    myList.erase(it);  // 删除第二个元素
    ```
*   **`clear()`**：删除链表中的所有元素。

    ```cpp
    myList.clear();  // 清空链表
    ```

**2.3 访问元素**

*   **`front()`**：返回链表头部的元素。

    ```cpp
    int firstElem = myList.front();
    ```
*   **`back()`**：返回链表尾部的元素。

    ```cpp
    int lastElem = myList.back();
    ```

**2.4 遍历元素**

*   **使用迭代器遍历**：

    ```cpp
    for (auto it = myList.begin(); it != myList.end(); ++it) {
        std::cout << *it << " ";
    }
    ```
*   **使用范围循环遍历**：

    ```cpp
    for (int elem : myList) {
        std::cout << elem << " ";
    }
    ```

**2.5 其他操作**

*   **`size()`**：返回链表中的元素个数。

    ```cpp
    std::cout << "Size: " << myList.size() << std::endl;
    ```
*   **`empty()`**：检查链表是否为空。如果链表为空，则返回 `true`。

    ```cpp
    if (myList.empty()) {
        std::cout << "List is empty" << std::endl;
    }
    ```
*   **`sort()`**：对链表中的元素进行排序。

    ```cpp
    myList.sort();  // 升序排序
    ```
*   **`reverse()`**：将链表中的元素顺序反转。

    ```cpp
    myList.reverse();  // 反转链表
    ```
*   **`merge(list<T>& otherList)`**：将 `otherList` 与当前链表合并，合并后 `otherList` 变为空。

    ```cpp
    std::list<int> otherList = {3, 6, 9};
    myList.merge(otherList);
    ```
*   **`unique()`**：移除链表中连续相等的重复元素。

    ```cpp
    myList.unique();  // 移除连续相同的元素
    ```

#### 3. **示例代码**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> myList = {10, 20, 30};

    // 插入元素
    myList.push_back(40);  // 尾部插入
    myList.push_front(5);  // 头部插入

    // 遍历链表
    for (const auto& elem : myList) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 访问头尾元素
    std::cout << "Front: " << myList.front() << std::endl;
    std::cout << "Back: " << myList.back() << std::endl;

    // 删除元素
    myList.pop_back();  // 删除尾部元素
    myList.pop_front(); // 删除头部元素

    // 排序和反转
    myList.sort();
    myList.reverse();

    // 遍历排序和反转后的链表
    for (const auto& elem : myList) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### 4. **`std::list` 的常见应用场景**

**1. 频繁插入/删除操作**

当需要频繁在序列的头部或中间进行插入和删除操作时，`std::list` 的双向链表结构能够提供常数时间的效率，而不像 `std::vector` 那样会引发元素移动和内存重新分配。

**2. 任务队列管理**

在任务调度系统中，可能需要随时对队列中的任务进行插入或删除操作。`std::list` 允许在任意位置高效地插入或移除任务。

**3. 链表操作**

有时在处理链表结构时，手动维护指针比较复杂，而使用 `std::list` 能够提供链表的所有功能（如插入、删除、排序、反转等）并且更安全。

**4. 需要动态增长的序列**

当序列的大小不确定并且可能频繁变化时，`std::list` 可以通过其链表特性高效地扩展而不需要像 `std::vector` 那样预分配或重新分配内存。

#### 5. **总结**

| 操作             | 描述          |
| -------------- | ----------- |
| `push_back()`  | 在链表尾部插入元素   |
| `push_front()` | 在链表头部插入元素   |
| `pop_back()`   | 删除链表尾部的元素   |
| `pop_front()`  | 删除链表头部的元素   |
| `insert()`     | 在指定位置插入元素   |
| `erase()`      | 删除指定位置的元素   |
| `front()`      | 返回链表头部的元素   |
| `back()`       | 返回链表尾部的元素   |
| `size()`       | 返回链表中的元素个数  |
| `empty()`      | 检查链表是否为空    |
| `sort()`       | 对链表中的元素进行排序 |
| `reverse()`    | 反转链表中的元素顺序  |
| `merge()`      | 合并两个链表      |
| `unique()`     | 移除连续的重复元素   |

`std::list` 适合在需要频繁插入和删除操作的场景下使用，尤其是在不需要随机访问的情况下，其效率比 `std::vector` 更高。
