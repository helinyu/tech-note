# 属性和方法

`std::priority_queue` 是 C++ STL 中的一个容器适配器，它提供了一些基本属性和方法，用于管理基于优先级的队列。以下是 `std::priority_queue` 的主要属性和方法：

## 1. **构造函数**

* **默认构造函数**：
  * `std::priority_queue<T>`：创建一个空的优先队列，其中 `T` 是存储的数据类型。
* **带容器和比较函数的构造函数**：
  * `std::priority_queue<T, Container, Compare>`：创建一个指定底层容器和比较方式的优先队列，`Container` 默认是 `std::vector<T>`，`Compare` 默认是 `std::less<T>`（大顶堆）。

## 2. **属性**

* **类型定义**：
  * `value_type`：存储的元素类型。
  * `container_type`：底层容器的类型（默认为 `std::vector<T>`）。
  * `size_type`：大小类型，用于存储优先队列中元素个数的数据类型。
  * `reference`：返回元素的引用类型。
  * `const_reference`：返回常量元素的引用类型。

## 3. **成员方法**

### **3.1 元素访问**

* **`top()`**：
  * **功能**：返回队列中优先级最高的元素（对于大顶堆是最大元素）。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::priority_queue<int> pq;
      pq.push(10);
      pq.push(5);
      pq.push(20);

      std::cout << pq.top();  // 输出 20
      ```

### **3.2 容量相关**

* **`empty()`**：
  * **功能**：检查优先队列是否为空。如果为空，返回 `true`，否则返回 `false`。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      if (pq.empty()) {
          std::cout << "Queue is empty";
      }
      ```
* **`size()`**：
  * **功能**：返回优先队列中元素的数量。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::cout << "Size: " << pq.size();  // 输出优先队列的元素数量
      ```

### **3.3 修改容器**

* **`push(const value_type& val)`**：
  * **功能**：将元素 `val` 插入到优先队列中。
  * **复杂度**：O(log n)，因为插入后需要维护堆结构。
  *   **示例**：

      ```cpp
      pq.push(15);  // 插入 15 到优先队列
      ```
* **`emplace(Args&&... args)`**：
  * **功能**：原位构造一个对象并插入到优先队列中，<mark style="color:red;">**避免了复制操作。**</mark>
  * **复杂度**：O(log n)。
  *   **示例**：

      ```cpp
      pq.emplace(25);  // 原位构造并插入 25
      ```
* **`pop()`**：
  * **功能**：移除优先级最高的元素（对于大顶堆是最大元素）。
  * **复杂度**：O(log n)，因为移除后需要维护堆结构。
  *   **示例**：

      ```cpp
      pq.pop();  // 移除优先级最高的元素
      ```

### **3.4 交换内容**

* **`swap(priority_queue& other)`**：
  * **功能**：与另一个优先队列 `other` 交换元素。
  * **复杂度**：O(1)。
  *   **示例**：

      ```cpp
      std::priority_queue<int> pq1, pq2;
      pq1.push(10);
      pq2.push(20);
      pq1.swap(pq2);  // 交换两个优先队列的内容
      ```

## 4. **比较函数**

`std::priority_queue` 的默认比较方式是 `std::less<T>`，即大顶堆。如果需要自定义优先级，可以传入自定义的比较器，例如使用 `std::greater<T>` 实现小顶堆。

**示例：使用 `std::greater<T>` 实现小顶堆**

```cpp
#include <queue>
#include <vector>
#include <iostream>

int main() {
    std::priority_queue<int, std::vector<int>, std::greater<int>> pq;  // 小顶堆
    pq.push(10);
    pq.push(5);
    pq.push(20);

    std::cout << pq.top();  // 输出 5
}
```

#### 5. **总结**

| 方法                            | 描述                 | 时间复杂度    |
| ----------------------------- | ------------------ | -------- |
| `top()`                       | 返回优先级最高的元素（不移除）。   | O(1)     |
| `push(const T& val)`          | 插入新元素，并重新调整堆。      | O(log n) |
| `emplace(Args&&... args)`     | 原位构造新元素并插入队列。      | O(log n) |
| `pop()`                       | 移除优先级最高的元素，并重新调整堆。 | O(log n) |
| `empty()`                     | 检查优先队列是否为空。        | O(1)     |
| `size()`                      | 返回优先队列中的元素数量。      | O(1)     |
| `swap(priority_queue& other)` | 交换两个优先队列的内容。       | O(1)     |

`std::priority_queue` 是一个灵活的容器，适用于需要管理具有优先级的任务或数据的场景，如贪心算法、调度系统等。
