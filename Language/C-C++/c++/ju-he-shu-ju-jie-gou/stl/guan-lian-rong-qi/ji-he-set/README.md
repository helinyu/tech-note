# 集合 set

在 C++ 中，`std::set` 是标准模板库（STL）中的一种关联容器，主要用于存储唯一的元素，并且自动对元素进行排序。`std::set` 是基于红黑树实现的，因此插入、删除和查找操作的时间复杂度都是 O(log n)。

#### **1. `std::set` 的主要特性**

* **唯一性**：`std::set` 中的元素是唯一的，不能有重复元素。
* **自动排序**：`std::set` 会根据元素的值自动进行排序，默认使用 `<` 运算符进行排序（升序）。
* **底层实现**：基于平衡二叉树（红黑树），查找、插入和删除的时间复杂度为 O(log n)。
* **键即值**：`std::set` 中没有键值对的概念，存储的是元素本身，元素既是键也是值。

#### **2. `std::set` 的主要方法**

**2.1 插入元素**

* **`insert(const value_type& val)`**：插入一个元素 `val`。如果元素已经存在，插入不会成功。
  *   示例：

      ```cpp
      std::set<int> mySet;
      mySet.insert(10);
      mySet.insert(20);
      mySet.insert(10);  // 插入失败，因为 10 已经存在
      ```
* **`emplace(Args&&... args)`**：直接在 `set` 中构造元素，可以避免拷贝操作。
  *   示例：

      ```cpp
      mySet.emplace(30);  // 直接插入 30
      ```

**2.2 查找元素**

* **`find(const Key& k)`**：查找键为 `k` 的元素，返回指向该元素的迭代器。如果没有找到，返回 `end()`。
  *   示例：

      ```cpp
      auto it = mySet.find(10);  // 查找 10
      if (it != mySet.end()) {
          std::cout << "Found: " << *it << std::endl;
      }
      ```
* **`count(const Key& k)`**：返回键 `k` 在集合中的数量。由于 `std::set` 中元素唯一，因此返回值只能是 `0` 或 `1`。
  *   示例：

      ```cpp
      if (mySet.count(10) > 0) {
          std::cout << "10 exists" << std::endl;
      }
      ```

**2.3 删除元素**

* **`erase(const Key& k)`**：删除键为 `k` 的元素，返回删除的元素数量（0 或 1）。
  *   示例：

      ```cpp
      mySet.erase(10);  // 删除元素 10
      ```
* **`erase(iterator pos)`**：删除迭代器 `pos` 指向的元素，返回下一个元素的迭代器。
  *   示例：

      ```cpp
      auto it = mySet.find(20);
      mySet.erase(it);  // 删除 20
      ```

**2.4 容量操作**

* **`size()`**：返回集合中元素的数量。
  *   示例：

      ```cpp
      std::cout << "Size: " << mySet.size() << std::endl;
      ```
* **`empty()`**：检查集合是否为空。如果为空返回 `true`。
  *   示例：

      ```cpp
      if (mySet.empty()) {
          std::cout << "Set is empty" << std::endl;
      }
      ```
* **`clear()`**：清空集合，删除所有元素。
  *   示例：

      ```cpp
      mySet.clear();  // 清空集合
      ```

**2.5 迭代器操作**

* **`begin()` 和 `end()`**：返回指向第一个元素和最后一个元素之后的位置的迭代器。
  *   示例：

      ```cpp
      for (auto it = mySet.begin(); it != mySet.end(); ++it) {
          std::cout << *it << std::endl;  // 输出集合中的元素
      }
      ```
* **`rbegin()` 和 `rend()`**：返回指向最后一个元素和第一个元素之前的位置的反向迭代器，用于反向遍历。
  *   示例：

      ```cpp
      for (auto it = mySet.rbegin(); it != mySet.rend(); ++it) {
          std::cout << *it << std::endl;  // 反向输出集合中的元素
      }
      ```

**2.6 范围操作**

* **`lower_bound(const Key& k)`**：返回指向第一个大于等于 `k` 的元素的迭代器。
  *   示例：

      ```cpp
      auto it = mySet.lower_bound(15);  // 返回第一个大于等于 15 的元素的迭代器
      ```
* **`upper_bound(const Key& k)`**：返回指向第一个大于 `k` 的元素的迭代器。
  *   示例：

      ```cpp
      auto it = mySet.upper_bound(15);  // 返回第一个大于 15 的元素的迭代器
      ```
* **`equal_range(const Key& k)`**：返回一对迭代器，表示键 `k` 的所有匹配元素的范围。在 `std::set` 中，键是唯一的，所以这两个迭代器要么指向同一元素，要么指向相同的位置。
  *   示例：

      ```cpp
      auto range = mySet.equal_range(20);
      ```

#### **3. 示例代码**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet;

    // 插入元素
    mySet.insert(10);
    mySet.insert(20);
    mySet.insert(30);

    // 查找元素
    if (mySet.count(20) > 0) {
        std::cout << "20 exists" << std::endl;
    }

    // 遍历元素
    for (const auto& elem : mySet) {
        std::cout << elem << std::endl;
    }

    // 删除元素
    mySet.erase(10);

    // 输出删除后的集合
    for (const auto& elem : mySet) {
        std::cout << elem << std::endl;
    }

    return 0;
}
```

#### **4. `std::set` 的常见使用场景**

* **唯一性要求的集合**：当需要存储一组唯一的元素时，比如存储学生学号、电话号码等。
* **有序性要求的集合**：当需要自动排序的集合时，比如存储数据并需要按自然顺序访问。
* **快速查找和删除的集合**：在需要快速查找、插入或删除元素的场景中，`std::set` 可以提供 O(log n) 的时间复杂度。

#### **5. 总结**

| 成员函数                            | 描述                        |
| ------------------------------- | ------------------------- |
| `insert(const value_type& val)` | 插入一个元素，若元素已存在则不插入。        |
| `emplace(Args&&... args)`       | 原位构造并插入元素，避免拷贝。           |
| `find(const Key& k)`            | 查找键为 `k` 的元素，返回指向该元素的迭代器。 |
| `count(const Key& k)`           | 返回键为 `k` 的元素数量（0 或 1）。    |
| `erase(const Key& k)`           | 删除键为 `k` 的元素。             |
| `size()`                        | 返回集合中元素的数量。               |
| `empty()`                       | 检查集合是否为空。                 |
| `clear()`                       | 清空集合，删除所有元素。              |
| `lower_bound(const Key& k)`     | 返回第一个小于等于 `k` 的元素的迭代器。    |
| `upper_bound(const Key& k)`     | 返回第一个大于 `k` 的元素的迭代器。      |
| `equal_range(const Key& k)`     | 返回与 `k` 匹配的元素的范围（两个迭代器）。  |

