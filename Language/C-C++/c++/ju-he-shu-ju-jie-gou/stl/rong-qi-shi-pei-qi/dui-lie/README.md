---
description: std::queue：
---

# 队列

在 C++ 中，`std::queue` 是标准模板库（STL）中的一种适配器容器，提供了一个先进先出（FIFO）的队列结构。`std::queue` 通常用于处理需要按顺序处理元素的场景，比如任务调度、广度优先搜索等。

## **1. `std::queue` 的主要特性**

* **先进先出（FIFO）**：元素按插入的顺序进行处理，最早插入的元素最先被移除。
* **适配器容器**：`std::queue` 是一个容器适配器，默认基于 `std::deque` 实现。你也可以使用其他序列容器（如 `std::list`）来作为底层存储。
* **访问限制**：只能访问队列的头部（最早插入的元素）和尾部（最近插入的元素），不能直接访问中间的元素。

## **2. `std::queue` 的主要方法**

**2.1 插入元素**

* **`push(const value_type& val)`**：将元素 `val` 插入到队列的尾部。
  *   示例：

      ```cpp
      std::queue<int> myQueue;
      myQueue.push(10);  // 插入 10
      myQueue.push(20);  // 插入 20
      ```
* **`emplace(Args&&... args)`**：直接在队列尾部构造元素，避免拷贝。
  *   示例：

      ```cpp
      myQueue.emplace(30);  // 直接插入 30
      ```

**2.2 访问元素**

* **`front()`**：返回队列头部的元素，即最早插入的元素。
  *   示例：

      ```cpp
      int frontElem = myQueue.front();  // 获取队列头部元素
      ```
* **`back()`**：返回队列尾部的元素，即最近插入的元素。
  *   示例：

      ```cpp
      int backElem = myQueue.back();  // 获取队列尾部元素
      ```

**2.3 删除元素**

* **`pop()`**：移除队列头部的元素，即最早插入的元素。该操作不会返回被移除的元素。
  *   示例：

      ```cpp
      myQueue.pop();  // 删除队列头部元素
      ```

**2.4 容量操作**

* **`size()`**：返回队列中的元素个数。
  *   示例：

      ```cpp
      std::cout << "Queue size: " << myQueue.size() << std::endl;
      ```
* **`empty()`**：检查队列是否为空。如果为空则返回 `true`。
  *   示例：

      ```cpp
      if (myQueue.empty()) {
          std::cout << "Queue is empty" << std::endl;
      }
      ```

**2.5 容器自定义**

* **自定义底层容器**：`std::queue` 默认使用 `std::deque` 作为底层容器。也可以使用其他序列容器如 `std::list`，但不能使用 `std::vector` 因为它不支持高效的头部插入和删除操作。
  *   使用 `std::list` 作为底层容器的示例：

      ```cpp
      std::queue<int, std::list<int>> myQueue;  // 使用 std::list 作为底层容器
      ```

## **3. 示例代码**

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    // 插入元素
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // 访问队列头部和尾部元素
    std::cout << "Front: " << myQueue.front() << std::endl;  // 输出 10
    std::cout << "Back: " << myQueue.back() << std::endl;    // 输出 30

    // 删除队列头部元素
    myQueue.pop();
    std::cout << "After pop, front: " << myQueue.front() << std::endl;  // 输出 20

    return 0;
}
```

## **4. `std::queue` 的常见使用场景**

**1. 任务调度**

`std::queue` 可用于任务调度系统，任务按添加的顺序被处理。例如在操作系统中，任务队列管理需要执行的进程，最早添加的进程会最先执行。

**2. 广度优先搜索（BFS）**

在图或树的广度优先搜索算法中，`std::queue` 被广泛用于存储需要遍历的节点。在 BFS 中，先访问的节点会首先从队列中移除，并且它的邻居节点会按照顺序加入队列。

**3. 生产者-消费者模型**

在多线程编程中，生产者-消费者模型可以使用 `std::queue` 实现。生产者不断向队列中添加任务，而消费者从队列中取出任务进行处理。

**4. 缓冲队列**

`std::queue` 可以用于处理数据流的缓冲区，在网络或文件处理的系统中，数据会按顺序到达并被处理。

## **5. 总结**

| 成员函数                 | 描述               |
| -------------------- | ---------------- |
| `push(const T& val)` | 将元素插入到队列的尾部。     |
| `emplace(Args&&...)` | 原位构造元素，并插入到队列尾部。 |
| `pop()`              | 删除队列头部的元素。       |
| `front()`            | 返回队列头部的元素。       |
| `back()`             | 返回队列尾部的元素。       |
| `size()`             | 返回队列中的元素个数。      |
| `empty()`            | 检查队列是否为空。        |

`std::queue` 提供了简洁的接口，用于处理先进先出的任务。在需要顺序处理数据时，`std::queue` 是非常有效的工具。
