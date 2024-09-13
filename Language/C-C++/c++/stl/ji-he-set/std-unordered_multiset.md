# std::unordered\_multiset

`std::unordered_multiset` 是 C++ 标准库中的一种关联容器，它允许元素重复，并且不对元素进行排序。其底层实现是哈希表，因此元素的查找、插入和删除操作的平均时间复杂度为 O(1)。相比于有序容器（如 `std::set` 和 `std::multiset`），`std::unordered_multiset` 在需要快速查找和处理大量重复元素的场景下表现出色。

#### **特点**

* **无序性**：`std::unordered_multiset` 不维护元素的顺序，元素的存储顺序与其插入顺序无关。
* **允许重复元素**：与 `std::unordered_set` 不同，`std::unordered_multiset` 允许多个相同的元素存在。
* **基于哈希表实现**：查找、插入和删除的时间复杂度在平均情况下是 O(1)，但最坏情况下为 O(n)。

#### **常见应用场景**

**1. 统计元素出现次数且不关心顺序**

当你需要统计元素的出现次数，且不需要对元素进行排序时，`std::unordered_multiset` 是一个合适的选择。由于它允许重复元素，你可以直接插入相同的元素来表示多次出现，而不需要维护额外的计数器。

**示例：统计文本中每个单词的出现次数**

```cpp
#include <iostream>
#include <unordered_multiset>
#include <string>
#include <sstream>

int main() {
    std::unordered_multiset<std::string> wordSet;
    std::string text = "this is a test this is only a test";
    std::istringstream iss(text);
    std::string word;

    // 插入每个单词
    while (iss >> word) {
        wordSet.insert(word);
    }

    // 输出每个单词的出现次数
    for (const auto& w : {"this", "is", "a", "test", "only"}) {
        std::cout << w << ": " << wordSet.count(w) << std::endl;
    }
    return 0;
}
```

此场景不关心单词的顺序，但我们希望能够快速统计每个单词的出现次数。

**2. 元素频繁重复且要求高效查找**

在需要存储大量重复元素并频繁查找是否存在的场景中，`std::unordered_multiset` 是一个很好的选择。哈希表的 O(1) 查找性能让它在处理频繁查询的任务中表现优异。

**示例：用户访问记录** 假设你正在开发一个网站并想要跟踪用户的访问行为，每次访问都记录到容器中。你只关心某个用户访问过几次，但不在乎访问顺序，这时可以使用 `std::unordered_multiset`。

```cpp
#include <iostream>
#include <unordered_multiset>
#include <string>

int main() {
    std::unordered_multiset<std::string> userVisits;

    // 模拟用户访问
    userVisits.insert("user1");
    userVisits.insert("user2");
    userVisits.insert("user1");
    userVisits.insert("user3");
    userVisits.insert("user1");

    // 查找 user1 访问了几次
    std::cout << "user1 visits: " << userVisits.count("user1") << std::endl;

    return 0;
}
```

在这个例子中，我们可以高效地统计每个用户的访问次数，而不需要处理元素的排序。

**3. 元素频繁插入、删除的场景**

在需要频繁插入和删除元素的场景中，`std::unordered_multiset` 提供了非常快的操作性能。由于哈希表的特性，插入和删除的操作都可以在平均 O(1) 的时间内完成。

**示例：处理交易日志** 如果你正在开发一个金融系统，需要对用户的交易进行实时跟踪和管理，你可以使用 `std::unordered_multiset` 来存储每笔交易。

```cpp
#include <iostream>
#include <unordered_multiset>
#include <string>

int main() {
    std::unordered_multiset<std::string> transactions;

    // 模拟交易记录
    transactions.insert("buy");
    transactions.insert("sell");
    transactions.insert("buy");
    transactions.insert("buy");
    transactions.insert("sell");

    // 删除一笔 'sell' 交易
    transactions.erase(transactions.find("sell"));

    // 统计 'buy' 交易的次数
    std::cout << "Buy transactions: " << transactions.count("buy") << std::endl;

    return 0;
}
```

在这个场景中，交易操作频繁且数量庞大，`std::unordered_multiset` 提供了快速的插入和删除功能。

**4. 快速判定某个元素是否存在**

在不关心元素顺序的集合中，`std::unordered_multiset` 提供了快速判定某个元素是否存在的能力，尤其是在处理大量数据时可以表现出优异的性能。

**示例：检测重复事件** 假设我们想检测某些事件是否已经发生过，可以使用 `std::unordered_multiset` 来快速判断。

```cpp
#include <iostream>
#include <unordered_multiset>
#include <string>

int main() {
    std::unordered_multiset<std::string> eventLog;

    // 插入一些事件
    eventLog.insert("login");
    eventLog.insert("download");
    eventLog.insert("upload");

    // 检测事件是否发生
    if (eventLog.count("login")) {
        std::cout << "Login event occurred." << std::endl;
    }

    return 0;
}
```

**5. 高效存储和访问无序数据**

在一些应用场景中，数据并不需要有序存储，只需要快速访问，这时候 `std::unordered_multiset` 是一个很好的选择。它通过哈希表管理元素，实现了高效的无序数据存储和快速访问。

#### **总结**

`std::unordered_multiset` 适用于以下场景：

* **快速统计频率**：在不关心顺序的情况下，需要快速统计元素出现的次数。
* **频繁查找和删除**：需要频繁查找和删除元素，并且要求操作时间复杂度接近 O(1)。
* **处理大量重复元素**：在处理包含大量重复元素的数据集合时，能够高效管理这些元素。
* **无需有序性要求**：如果不需要有序存储数据，并且主要关注快速查找和操作性能，那么 `std::unordered_multiset` 是理想选择。

相比 `std::set` 和 `std::multiset`，`std::unordered_multiset` 提供了更高效的插入、删除和查找操作，非常适合对无序且可能有重复元素的集合进行处理。
