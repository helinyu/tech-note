# C++

在 C++ 中，`priority_queue` 是一个常用的数据结构，提供了一种高效的方式来管理优先级队列。

#### 引入头文件

首先，我们需要引入头文件：

```cpp
#include <iostream>
#include <queue>
#include <vector>
```

#### 创建 `priority_queue`

**默认创建最大优先队列**

默认情况下，`priority_queue` 是一个最大优先队列，即队列中的元素以降序排列，堆顶元素是最大值。

```cpp
std::priority_queue<int> maxPQ;
```

<mark style="color:red;">**创建最小优先队列**</mark>

要创建一个最小优先队列，可以使用 `std::greater<T>` 或自定义比较函数。

```cpp
std::priority_queue<int, std::vector<int>, std::greater<int>> minPQ;
```

#### `priority_queue` 的常用方法

以下是 `priority_queue` 的常用方法及其说明：

1. **`push(const T& value)`**：将元素插入优先队列。
2. **`pop()`**：移除优先队列中优先级最高的元素。
3. **`top()`**：返回优先队列中优先级最高的元素，但不移除它。
4. **`empty()`**：检查优先队列是否为空。
5. **`size()`**：返回优先队列中元素的数量。

####

{% hint style="info" %}
注意：

不同的语言中，可能就是push、pop、top 这三个函数的名字不一样罢了。
{% endhint %}

#### 示例代码

以下是一个完整的示例，展示了如何使用 `priority_queue`：

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // 创建一个最大优先队列
    std::priority_queue<int> maxPQ;

    // 插入元素
    maxPQ.push(3);
    maxPQ.push(1);
    maxPQ.push(5);
    maxPQ.push(2);

    // 输出优先队列的大小
    std::cout << "Size of maxPQ: " << maxPQ.size() << std::endl;

    // 获取并移除优先级最高的元素
    while (!maxPQ.empty()) {
        std::cout << maxPQ.top() << " ";  // 输出：5 3 2 1
        maxPQ.pop();
    }

    std::cout << std::endl;

    // 创建一个最小优先队列
    std::priority_queue<int, std::vector<int>, std::greater<int>> minPQ;

    // 插入元素
    minPQ.push(3);
    minPQ.push(1);
    minPQ.push(5);
    minPQ.push(2);

    // 输出优先队列的大小
    std::cout << "Size of minPQ: " << minPQ.size() << std::endl;

    // 获取并移除优先级最低的元素
    while (!minPQ.empty()) {
        std::cout << minPQ.top() << " ";  // 输出：1 2 3 5
        minPQ.pop();
    }

    return 0;
}
```

#### 自定义比较函数

如果你需要更复杂的优先级逻辑，可以通过自定义比较函数来实现。例如，以下代码展示了如何使用仿函数来创建优先队列：

<pre class="language-cpp"><code class="lang-cpp"><strong>#include &#x3C;iostream>
</strong>#include &#x3C;queue>
#include &#x3C;vector>

struct CustomCompare {
    bool operator()(int a, int b) {
        return a > b;  
    }
};

int main() {
    // 使用自定义比较函数创建优先队列
    // 这时使用了上面的是小顶堆
    std::priority_queue&#x3C;int, std::vector&#x3C;int>, CustomCompare> customPQ;

    // 插入元素
    customPQ.push(3);
    customPQ.push(1);
    customPQ.push(5);
    customPQ.push(2);

    // 获取并移除优先级最低的元素
    while (!customPQ.empty()) {
        std::cout &#x3C;&#x3C; customPQ.top() &#x3C;&#x3C; " ";  // 输出：1 2 3 5
        customPQ.pop();
    }

    return 0;
}
</code></pre>

#### 总结

C++ 中的 `priority_queue` 提供了一种高效的方式来管理优先级队列。通过使用不同的比较函数，你可以轻松地实现最大优先队列、最小优先队列以及基于自定义数据类型的优先队列。理解并掌握 `priority_queue` 的使用方法，将有助于你在各种应用场景中有效地管理和处理数据。
