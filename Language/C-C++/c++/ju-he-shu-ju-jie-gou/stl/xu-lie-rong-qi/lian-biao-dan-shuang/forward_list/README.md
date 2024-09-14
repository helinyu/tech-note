# forward\_list

`std::forward_list` 是 C++11 引入的 STL 容器，它实现了单向链表（Singly Linked List），与 `std::list` 不同的是，`std::forward_list` 只有前向指针，不能向后遍历，因此它的空间开销比 `std::list` 更小。

#### 1. **`std::forward_list` 的主要特点**

* **单向链表**：`std::forward_list` 是单向链表，它只提供对下一个元素的访问，即只能从头到尾进行遍历，无法反向遍历。
* **空间效率更高**：由于每个节点只维护一个前向指针，所以与 `std::list` 相比，`std::forward_list` 的内存开销更低。
* **不支持随机访问**：`std::forward_list` 不像 `std::vector` 或 `std::deque` 那样支持随机访问。为了找到某个特定元素，需要从头开始遍历链表。
* **常数时间的插入和删除**：与 `std::list` 类似，`std::forward_list` 也支持常数时间内的插入和删除操作，特别是在链表头部和中间位置。

#### 2. **`std::forward_list` 的常用方法**

**2.1 插入元素**

*   **`push_front(const T& value)`**：在链表头部插入元素 `value`。

    ```cpp
    std::forward_list<int> flist;
    flist.push_front(10);  // 在头部插入 10
    flist.push_front(20);  // 在头部插入 20
    ```
*   **`emplace_front(Args&&... args)`**：在链表头部原位构造元素。

    ```cpp
    flist.emplace_front(30);  // 在头部原位构造 30
    ```
*   **`insert_after(iterator position, const T& value)`**：在指定迭代器 `position` 之后插入元素 `value`。

    ```cpp
    auto it = flist.begin();
    flist.insert_after(it, 25);  // 在第一个元素之后插入 25
    ```
*   **`emplace_after(iterator position, Args&&... args)`**：在指定迭代器 `position` 之后原位构造元素。

    ```cpp
    flist.emplace_after(it, 35);  // 在第一个元素之后原位构造 35
    ```

**2.2 删除元素**

*   **`pop_front()`**：删除链表头部的元素。

    ```cpp
    flist.pop_front();  // 删除头部元素
    ```
*   **`erase_after(iterator position)`**：删除迭代器 `position` 之后的元素。

    ```cpp
    flist.erase_after(it);  // 删除第一个元素之后的元素
    ```
*   **`clear()`**：删除链表中的所有元素。

    ```cpp
    flist.clear();  // 清空链表
    ```

**2.3 访问元素**

*   **`front()`**：返回链表头部的元素。

    ```cpp
    int firstElem = flist.front();
    ```

**2.4 遍历元素**

*   **使用迭代器遍历**：

    ```cpp
    for (auto it = flist.begin(); it != flist.end(); ++it) {
        std::cout << *it << " ";
    }
    ```
*   **使用范围循环遍历**：

    ```cpp
    for (int elem : flist) {
        std::cout << elem << " ";
    }
    ```

**2.5 其他操作**

*   **`empty()`**：检查链表是否为空。如果链表为空，则返回 `true`。

    ```cpp
    if (flist.empty()) {
        std::cout << "Forward list is empty" << std::endl;
    }
    ```
*   **`max_size()`**：返回链表能容纳的最大元素数量。

    ```cpp
    std::cout << "Max size: " << flist.max_size() << std::endl;
    ```
*   **`resize(size_type n)`**：调整链表的大小。如果链表当前大小小于 `n`，则插入默认值填充；如果大于 `n`，则移除多余的元素。

    ```cpp
    flist.resize(5);
    ```
*   **`sort()`**：对链表中的元素进行升序排序。

    ```cpp
    flist.sort();
    ```
*   **`reverse()`**：将链表中的元素顺序反转。

    ```cpp
    flist.reverse();
    ```
*   **`merge(forward_list<T>& other)`**：将 `other` 链表中的元素合并到当前链表中，合并后 `other` 变为空。

    ```cpp
    std::forward_list<int> otherList = {5, 15, 25};
    flist.merge(otherList);
    ```
*   **`unique()`**：移除链表中连续相等的重复元素。

    ```cpp
    flist.unique();
    ```

#### 3. **示例代码**

```cpp
#include <iostream>
#include <forward_list>

int main() {
    std::forward_list<int> flist = {10, 20, 30};

    // 插入元素
    flist.push_front(5);   // 头部插入
    flist.insert_after(flist.begin(), 15); // 在第一个元素后插入 15

    // 遍历链表
    for (const auto& elem : flist) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 访问头部元素
    std::cout << "Front: " << flist.front() << std::endl;

    // 删除元素
    flist.pop_front();  // 删除头部元素

    // 排序和反转
    flist.sort();
    flist.reverse();

    // 遍历排序和反转后的链表
    for (const auto& elem : flist) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### 4. **`std::forward_list` 的常见应用场景**

**1. 轻量级链表结构**

`std::forward_list` 适合在需要链表结构，但对内存消耗和性能有较高要求的场景。由于它比 `std::list` 节省更多内存，因此适合嵌入式系统或内存受限的环境。

**2. 需要频繁插入/删除的场景**

与 `std::list` 类似，`std::forward_list` 适合需要频繁在序列头部或中间插入/删除元素的场景，比如任务调度、消息传递系统等。

**3. 排序、合并、去重**

在需要对数据进行排序、合并或去重的场景下，`std::forward_list` 也提供了非常高效的操作方式。

#### 5. **总结**

| 操作               | 描述          |
| ---------------- | ----------- |
| `push_front()`   | 在链表头部插入元素   |
| `insert_after()` | 在指定位置之后插入元素 |
| `erase_after()`  | 删除指定位置之后的元素 |
| `pop_front()`    | 删除链表头部的元素   |
| `front()`        | 返回链表头部的元素   |
| `empty()`        | 检查链表是否为空    |
| `sort()`         | 对链表中的元素进行排序 |
| `reverse()`      | 反转链表中的元素顺序  |
| `merge()`        | 合并两个链表      |
| `unique()`       | 移除连续的重复元素   |

`std::forward_list` 是一个内存高效的单向链表，适合在需要链表功能但希望降低内存开销的场景中使用。
