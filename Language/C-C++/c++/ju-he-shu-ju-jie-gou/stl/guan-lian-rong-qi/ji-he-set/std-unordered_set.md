# std::unordered\_set

它存储一组唯一的元素，但不保证元素的存储顺序。以下是一些常见的应用场景：

**一、快速查找唯一元素**

1. 数据验证和去重：
   * 当处理大量数据时，需要快速判断一个元素是否已经存在于集合中，并且去除重复元素。`std::unordered_set`提供了快速的插入和查找操作，平均时间复杂度为常数时间。
   * 例如，在读取一个大型文本文件时，可以使用`std::unordered_set`来存储已经处理过的单词，以避免重复处理相同的单词。
   *   以下是一个简单的示例：

       ```cpp
       std::unordered_set<std::string> uniqueWords;
       std::string word;
       while (std::cin >> word) {
           if (uniqueWords.find(word) == uniqueWords.end()) {
               // 单词是新的，进行处理
               uniqueWords.insert(word);
           }
       }
       ```
2. 缓存和过滤：
   * 在一些应用中，需要快速判断一个元素是否已经在缓存中，或者过滤掉已经处理过的元素。`std::unordered_set`可以作为一个高效的缓存或过滤器，快速判断元素的存在性。
   * 例如，在一个网络爬虫中，可以使用`std::unordered_set`来存储已经访问过的网页 URL，以避免重复访问。
   *   以下是一个示例：

       ```cpp
       std::unordered_set<std::string> visitedUrls;
       std::string url;
       while (/* 还有未访问的 URL 来源 */) {
           url = /* 获取下一个 URL */;
           if (visitedUrls.find(url) == visitedUrls.end()) {
               // URL 未被访问过，进行处理
               visitedUrls.insert(url);
           }
       }
       ```

**二、集合操作**

1. 并集、交集和差集：
   * 虽然`std::unordered_set`没有直接提供集合操作的函数，但可以通过手动实现来进行并集、交集和差集的计算。
   *   例如，计算两个集合的并集：

       ```cpp
       std::unordered_set<int> set1 = {1, 2, 3, 4};
       std::unordered_set<int> set2 = {3, 4, 5, 6};
       std::unordered_set<int> unionSet;
       for (const int& element : set1) {
           unionSet.insert(element);
       }
       for (const int& element : set2) {
           unionSet.insert(element);
       }
       ```
   * 类似地，可以实现交集和差集的计算。
2. 成员关系判断：
   * 快速判断一个元素是否属于一个集合。由于`std::unordered_set`的查找操作平均时间复杂度为常数时间，因此在处理大量元素时非常高效。
   *   例如：

       ```cpp
       std::unordered_set<int> mySet = {1, 2, 3, 4};
       bool isMember = (mySet.find(3)!= mySet.end());
       ```

**三、作为哈希表的替代**

1. 简单的键值存储：
   * 如果只需要存储唯一的键，而不需要关联的值，可以使用`std::unordered_set`作为一个简单的哈希表替代。
   *   例如，存储一组唯一的用户名：

       ```cpp
       std::unordered_set<std::string> usernames;
       usernames.insert("user1");
       usernames.insert("user2");
       // 检查用户名是否存在
       bool exists = (usernames.find("user1")!= usernames.end());
       ```
2. 快速访问特定元素：
   * 当需要快速访问特定的元素时，可以使用`std::unordered_set`的查找操作来快速定位元素。
   * 例如，在一个游戏中，存储已经出现的敌人类型，以便快速判断某个敌人类型是否已经出现过。
   *   以下是一个示例：

       ```cpp
       std::unordered_set<std::string> enemyTypes;
       enemyTypes.insert("zombie");
       enemyTypes.insert("skeleton");
       // 检查特定敌人类型是否存在
       bool exists = (enemyTypes.find("zombie")!= enemyTypes.end());
       ```
