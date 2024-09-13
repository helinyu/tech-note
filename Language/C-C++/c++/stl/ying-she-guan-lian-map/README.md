# 映射（关联）map

在 C++ STL（标准模板库）中，`std::map` 是一种**关联容器**，用于存储键值对。`std::map` 中的每个元素都由唯一的键和关联的值组成，并且根据键的顺序自动排序（默认是升序）。它基于**红黑树**实现，提供高效的插入、删除和查找操作。

## 1. **基本特点**

* **键值对存储**：`std::map` 中的每个元素都是一个 `std::pair<const Key, T>`，其中 `Key` 是键，`T` 是值。
* **键的唯一性**：`std::map` 中的键必须唯一，重复的键会覆盖原来的值。
* **自动排序**：`std::map` 中的键按照某种顺序进行排序，默认使用 `std::less`（即按升序排序）。可以通过自定义比较器修改排序方式。
* **底层实现**：基于**红黑树**，确保查找、插入和删除的时间复杂度为 O(log n)。

## 2. **基本操作**

### **2.1 插入操作**

* **`insert(const value_type& val)`**：
  * 插入键值对，如果键已经存在，则插入失败。
  * 返回一个 `pair<iterator, bool>`，`iterator` 指向插入的位置，`bool` 表示是否成功插入。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      std::map<int, std::string> myMap;
      myMap.insert(std::make_pair(1, "apple"));
      myMap.insert({2, "banana"});
      ```
* **`operator[]`**：
  * 通过键访问元素，如果键不存在，则创建一个默认值。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      myMap[3] = "cherry";  // 如果键 3 不存在，创建并插入默认值
      ```

### **2.2 查找操作**

* **`find(const Key& k)`**：
  * 查找键 `k`，返回指向对应键值对的迭代器，如果未找到则返回 `end()`。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      auto it = myMap.find(1);
      if (it != myMap.end()) {
          std::cout << "Found: " << it->second << std::endl;
      }
      ```
* **`count(const Key& k)`**：
  * 返回键 `k` 是否存在的数量，`std::map` 中键是唯一的，所以返回值要么是 `0`（不存在），要么是 `1`（存在）。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      if (myMap.count(1) > 0) {
          std::cout << "Key 1 exists" << std::endl;
      }
      ```

### **2.3 删除操作**

* **`erase(iterator pos)`**：
  * 删除指定位置的元素，返回下一个元素的迭代器。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      auto it = myMap.find(2);
      if (it != myMap.end()) {
          myMap.erase(it);  // 删除键为 2 的元素
      }
      ```
* **`erase(const Key& k)`**：
  * 根据键 `k` 删除元素，返回删除的元素数量（只能是 0 或 1）。
  * 时间复杂度：O(log n)。
  *   示例：

      ```cpp
      myMap.erase(1);  // 删除键为 1 的元素
      ```

### **2.4 其他操作**

* **`size()`**：
  * 返回 `map` 中元素的数量。
  * 时间复杂度：O(1)。
  *   示例：

      ```cpp
      std::cout << "Size: " << myMap.size() << std::endl;  // 输出 map 中元素数量
      ```
* **`empty()`**：
  * 检查 `map` 是否为空，如果为空返回 `true`。
  * 时间复杂度：O(1)。
  *   示例：

      ```cpp
      if (myMap.empty()) {
          std::cout << "Map is empty" << std::endl;
      }
      ```
* **`clear()`**：
  * 清除所有元素。
  * 时间复杂度：O(n)。
  *   示例：

      ```cpp
      myMap.clear();  // 清空 map
      ```
* **`swap(map& other)`**：
  * 交换两个 `map` 的内容。
  * 时间复杂度：O(1)。
  *   示例：

      ```cpp
      std::map<int, std::string> myMap2;
      myMap.swap(myMap2);  // 交换 myMap 和 myMap2 的内容
      ```

## 3. **遍历操作**

`std::map` 支持使用迭代器遍历元素。

**正向遍历：**

```cpp
for (const auto& pair : myMap) {
    std::cout << pair.first << ": " << pair.second << std::endl;
}
```

**反向遍历：**

```cpp
for (auto it = myMap.rbegin(); it != myMap.rend(); ++it) {
    std::cout << it->first << ": " << it->second << std::endl;
}
```

## 4. **自定义排序**

`std::map` 默认使用 `std::less<Key>` 作为排序准则，键按照升序排序。如果需要自定义排序，可以提供一个自定义的比较函数或函数对象。

**自定义比较器示例（降序排序）：**

```cpp
struct Descending {
    bool operator()(const int& a, const int& b) const {
        return a > b;
    }
};

std::map<int, std::string, Descending> myMap;  // 使用降序排序
```

## 5. **常用成员函数汇总**

| 成员函数                            | 描述                           |
| ------------------------------- | ---------------------------- |
| `insert(const value_type& val)` | 插入键值对。                       |
| `operator[](const Key& k)`      | 通过键访问元素，如果不存在则插入默认值。         |
| `find(const Key& k)`            | 查找键为 `k` 的元素，返回迭代器。          |
| `count(const Key& k)`           | 返回键为 `k` 的元素个数（0 或 1）。       |
| `erase(const Key& k)`           | 删除键为 `k` 的元素。                |
| `size()`                        | 返回元素的数量。                     |
| `empty()`                       | 检查是否为空。                      |
| `clear()`                       | 删除所有元素。                      |
| `swap(map& other)`              | 交换两个 `map` 的内容。              |
| `begin()`, `end()`              | 返回正向迭代器，指向第一个元素和最后一个元素之后的位置。 |
| `rbegin()`, `rend()`            | 返回反向迭代器，指向最后一个元素和第一个元素之前的位置。 |

## 6. **示例代码**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> myMap;

    // 插入元素
    myMap.insert(std::make_pair(1, "apple"));
    myMap[2] = "banana";
    myMap[3] = "cherry";

    // 查找元素
    if (myMap.find(1) != myMap.end()) {
        std::cout << "Found key 1: " << myMap[1] << std::endl;
    }

    // 遍历元素
    for (const auto& pair : myMap) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    // 删除元素
    myMap.erase(2);

    // 输出删除后的 map
    for (const auto& pair : myMap) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

## 7. **总结**

* `std::map` 是一个关联容器，基于红黑树实现，键唯一且自动排序。
* 主要操作的时间复杂度为 O(log n)，适合用于快速查找、插入和删除操作。
* 提供了丰富的接口用于操作键值对，并且可以自定义键的排序方式。
