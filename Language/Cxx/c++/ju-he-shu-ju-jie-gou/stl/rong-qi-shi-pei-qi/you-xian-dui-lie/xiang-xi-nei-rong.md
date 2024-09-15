# 详细内容

`std::priority_queue` 是C++ STL中提供的一种容器适配器，用于实现优先队列。它的<mark style="color:red;">特点是元素按照优先级排序，默认情况下是</mark><mark style="color:red;">**大顶堆**</mark>，即每次访问或移除的都是当前最大元素。也可以通过指定比较函数，实现**小顶堆**或自定义优先级的队列。

## 1. **基本特点**

* 默认情况下，`std::priority_queue`是基于最大堆（大顶堆）的优先队列，最大元素具有最高优先级。
* 底层通常使用 `std::vector` 作为存储容器，并通过堆算法（heap）来维护优先级顺序。
* 操作的时间复杂度为 O(log n)，因为每次插入和删除操作都需要重新调整堆。

## 2. **定义与基本操作**

### **2.1 定义优先队列**

```cpp
#include <queue>
#include <iostream>

int main() {
    std::priority_queue<int> pq;  // 默认情况下是大顶堆
    pq.push(10);
    pq.push(5);
    pq.push(20);
    
    std::cout << "Top element: " << pq.top() << std::endl;  // 输出 20
    pq.pop();  // 移除最大元素 20
    
    std::cout << "Top element: " << pq.top() << std::endl;  // 输出 10
}
```

### **2.2 操作方法**

* **`push()`**：将元素插入优先队列。
* **`pop()`**：移除当前优先级最高的元素（对于大顶堆来说是最大元素）。
* **`top()`**：返回优先级最高的元素，但不移除它。
* **`empty()`**：判断优先队列是否为空。
* **`size()`**：返回优先队列中元素的个数。

**示例：**

```cpp
std::priority_queue<int> pq;
pq.push(1);
pq.push(50);
pq.push(25);

std::cout << "Size: " << pq.size() << std::endl;  // 输出 3
std::cout << "Top element: " << pq.top() << std::endl;  // 输出 50
pq.pop();
std::cout << "Top element after pop: " << pq.top() << std::endl;  // 输出 25
```

## 3. **自定义优先级**

默认情况下，`std::priority_queue` 是大顶堆。如果希望实现小顶堆或自定义优先级，需要指定比较函数或仿函数。

### **3.1 小顶堆的实现**

可以通过指定 `std::greater<T>` 作为比较函数，将优先队列变为小顶堆。

```cpp
#include <queue>
#include <vector>
#include <functional>  // for std::greater

int main() {
    // 使用std::greater<int>来实现小顶堆
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
    minHeap.push(10);
    minHeap.push(5);
    minHeap.push(20);

    std::cout << "Top element in min-heap: " << minHeap.top() << std::endl;  // 输出 5
    minHeap.pop();
    std::cout << "Top element after pop: " << minHeap.top() << std::endl;  // 输出 10
}
```

### **3.2 自定义比较规则**

如果需要对复杂类型的对象进行排序，可以自定义比较规则。可以通过传入自定义的仿函数或函数对象来实现。

**示例：自定义比较函数**

```cpp
#include <queue>
#include <vector>
#include <iostream>

struct Person {
    int age;
    std::string name;

    // 自定义比较函数，优先级按照年龄从大到小排序
    bool operator<(const Person& other) const {
        return age < other.age;
    }
};

int main() {
    std::priority_queue<Person> pq;
    pq.push({30, "Alice"});
    pq.push({25, "Bob"});
    pq.push({35, "Charlie"});

    std::cout << "Oldest person: " << pq.top().name << std::endl;  // 输出 Charlie
    pq.pop();
    std::cout << "Next oldest person: " << pq.top().name << std::endl;  // 输出 Alice
}
```

在这个例子中，我们使用了自定义结构体 `Person` 并通过重载 `<` 运算符来定义优先队列的排序规则。

## 4. **复杂度**

* **插入元素（`push()`）**：时间复杂度为 O(log n)，因为每次插入时需要重新维护堆结构。
* **删除元素（`pop()`）**：时间复杂度为 O(log n)，移除顶元素后也需要重新维护堆。
* **访问最大或最小元素（`top()`）**：时间复杂度为 O(1)，因为顶元素始终是堆顶，不需要任何操作。

## 5. **适用场景**

* **任务调度**：当多个任务具有不同的优先级时，可以使用 `std::priority_queue` 按照优先级执行任务。
* **贪心算法**：很多<mark style="color:red;">**贪心算法**</mark>，如<mark style="color:orange;">哈夫曼编码、Dijkstra 最短路径算法</mark>等，都依赖于优先队列来获取当前的最优解。
* **实时数据流**：处理需要频繁获取最值的场景（如实时计算最大或最小元素）。

## 6. **总结**

* `std::priority_queue` 是一个强大的容器适配器，默认情况下实现大顶堆（最大优先队列）。
* 通过自定义比较规则，可以实现小顶堆或其他自定义优先级队列。
* 适用于需要频繁处理具有优先级的元素集合的场景，如<mark style="color:red;">**调度、排序、贪心算法**</mark>等。
