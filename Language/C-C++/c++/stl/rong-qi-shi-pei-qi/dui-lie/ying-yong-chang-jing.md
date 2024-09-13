# 应用场景

`std::queue` 在开发中具有广泛的应用，特别是在需要遵循“先进先出”（FIFO）规则的场景下。以下是一些常见的 `std::queue` 应用场景：

#### 1. **任务调度（Task Scheduling）**

在操作系统或应用程序中，常常需要对任务进行调度。`std::queue` 能够很好地模拟任务队列，任务按照添加的顺序被执行。任务调度系统的核心思路是：

* 新任务加入队列尾部。
* 执行任务时，从队列头部取出任务并进行处理。

```cpp
std::queue<std::string> taskQueue;
taskQueue.push("Task1");
taskQueue.push("Task2");

// 处理任务
while (!taskQueue.empty()) {
    std::cout << "Processing " << taskQueue.front() << std::endl;
    taskQueue.pop();
}
```

#### 2. **广度优先搜索（BFS）**

`std::queue` 是广度优先搜索算法（BFS）的关键数据结构。在图或者树的遍历中，BFS 会按层次逐步访问节点。遍历的顺序是：

* 将起始节点放入队列。
* 依次访问队列中的节点，并将其相邻的未访问节点加入队列。

```cpp
#include <iostream>
#include <queue>
#include <vector>

void bfs(int start, const std::vector<std::vector<int>>& graph) {
    std::queue<int> q;
    std::vector<bool> visited(graph.size(), false);

    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        std::cout << "Visited: " << node << std::endl;

        // 遍历相邻节点
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}

int main() {
    std::vector<std::vector<int>> graph = {
        {1, 2},  // 0 号节点的邻居
        {0, 3},  // 1 号节点的邻居
        {0, 3},  // 2 号节点的邻居
        {1, 2}   // 3 号节点的邻居
    };

    bfs(0, graph);
    return 0;
}
```

在这个例子中，我们使用 `std::queue` 实现了广度优先搜索，按层次访问图中的节点。

#### 3. **生产者-消费者模型**

在多线程编程中，`std::queue` 常用于生产者-消费者模式。生产者线程将任务或数据加入队列，消费者线程从队列中取出任务进行处理。`std::queue` 在该模式中作为共享缓冲区，确保任务按顺序处理。

```cpp
#include <iostream>
#include <queue>
#include <thread>
#include <mutex>
#include <condition_variable>

std::queue<int> dataQueue;
std::mutex mtx;
std::condition_variable cv;

void producer(int n) {
    for (int i = 0; i < n; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        dataQueue.push(i);
        std::cout << "Produced: " << i << std::endl;
        cv.notify_one();  // 通知消费者
    }
}

void consumer() {
    while (true) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [] { return !dataQueue.empty(); });

        int data = dataQueue.front();
        dataQueue.pop();
        std::cout << "Consumed: " << data << std::endl;
        
        if (data == -1) break;  // 消费结束信号
    }
}

int main() {
    std::thread t1(producer, 10);
    std::thread t2(consumer);

    t1.join();
    t2.join();

    return 0;
}
```

这里展示了生产者线程生成数据，消费者线程从队列中取出数据进行处理的例子。

#### 4. **事件处理系统**

在事件驱动的系统中，事件按到达的顺序被处理。事件处理系统会将外部输入（如用户点击、键盘输入等）放入事件队列，事件处理器按顺序从队列中获取事件并进行处理。

```cpp
std::queue<std::string> eventQueue;

// 添加事件
eventQueue.push("Mouse Clicked");
eventQueue.push("Key Pressed");

// 处理事件
while (!eventQueue.empty()) {
    std::string event = eventQueue.front();
    std::cout << "Handling event: " << event << std::endl;
    eventQueue.pop();
}
```

#### 5. **消息传递系统**

在通信或分布式系统中，消息按顺序发送和处理。消息可以先进入一个队列，消息处理器会按照先后顺序从队列中取出消息进行处理。这种模型在聊天系统、消息队列服务中非常常见。

```cpp
std::queue<std::string> messageQueue;
messageQueue.push("Message 1");
messageQueue.push("Message 2");

while (!messageQueue.empty()) {
    std::cout << "Processing: " << messageQueue.front() << std::endl;
    messageQueue.pop();
}
```

#### 6. **网络数据包处理**

在网络通信中，接收到的数据包可能需要按顺序处理，`std::queue` 可以用于存储接收到的数据包，按顺序从队列中取出并处理数据。

```cpp
std::queue<std::string> packetQueue;

// 收到数据包
packetQueue.push("Packet 1");
packetQueue.push("Packet 2");

// 处理数据包
while (!packetQueue.empty()) {
    std::string packet = packetQueue.front();
    std::cout << "Processing: " << packet << std::endl;
    packetQueue.pop();
}
```

#### 7. **打印任务队列**

在打印管理系统中，打印任务会进入一个队列，按顺序发送到打印机。任务可以按照提交的顺序进行打印，这符合 `std::queue` 的 FIFO 原则。

```cpp
std::queue<std::string> printQueue;
printQueue.push("Document 1");
printQueue.push("Document 2");

while (!printQueue.empty()) {
    std::cout << "Printing: " << printQueue.front() << std::endl;
    printQueue.pop();
}
```

#### 8. **网页浏览历史**

在网页浏览器中，用户的浏览历史也可以用队列进行管理。用户访问网页的顺序被存入队列，随后可以按顺序回退到之前浏览过的网页。

```cpp
std::queue<std::string> browserHistory;
browserHistory.push("Page 1");
browserHistory.push("Page 2");

while (!browserHistory.empty()) {
    std::cout << "Visited: " << browserHistory.front() << std::endl;
    browserHistory.pop();
}
```

#### 总结

`std::queue` 适用于以下常见开发场景：

1. **任务调度**：按顺序执行任务。
2. **广度优先搜索**：按层次遍历图或树。
3. **生产者-消费者模型**：在多线程环境下高效处理任务。
4. **事件处理系统**：按顺序处理外部输入事件。
5. **消息传递系统**：保证消息按发送顺序处理。
6. **网络数据包处理**：按顺序处理接收到的数据包。
7. **打印任务队列**：按顺序执行打印任务。
8. **网页浏览历史**：管理用户的浏览顺序。

`std::queue` 在处理顺序性任务时非常有用，尤其在需要先进先出的场景下能发挥重要作用。
