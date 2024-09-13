# std::multiset

`std::multiset`是 C++ 标准模板库中的关联容器，它允许存储重复的元素，并按照特定的严格弱序进行排序。以下是一些常见的应用场景：

**一、统计元素出现次数**

1. 文本分析：
   * 在文本处理中，可能需要统计某个单词或字符在文本中出现的次数。`std::multiset`可以方便地存储文本中的单词或字符，并快速统计它们的出现次数。
   *   例如，统计一篇文章中每个单词的出现次数：

       ```cpp
       std::string text = "this is a sample text. this is another sample.";
       std::istringstream iss(text);
       std::string word;
       std::multiset<std::string> wordSet;
       while (iss >> word) {
           wordSet.insert(word);
       }
       for (const auto& w : wordSet) {
           std::cout << w << ": " << std::count(wordSet.begin(), wordSet.end(), w) << std::endl;
       }
       ```
2. 数据监测：
   * 在实时数据监测系统中，可能需要统计特定事件或数据值的出现次数。`std::multiset`可以存储这些数据值，并快速统计它们的出现频率。
   *   比如，监测一个传感器网络中特定传感器值的出现次数：

       ```cpp
       std::multiset<int> sensorValues;
       // 假设不断有传感器值传入
       sensorValues.insert(10);
       sensorValues.insert(15);
       sensorValues.insert(10);
       int valueToCount = 10;
       std::cout << valueToCount << " appears " << std::count(sensorValues.begin(), sensorValues.end(), valueToCount) << " times." << std::endl;
       ```

**二、处理有序但可重复的数据集合**

1. 成绩管理系统：
   * 在一个成绩管理系统中，可能需要存储学生的成绩。成绩可以重复出现，并且需要按照升序或降序进行排序。`std::multiset`可以满足这个需求，方便地存储成绩并进行排序和查询。
   *   例如：

       ```cpp
       std::multiset<int> scores;
       scores.insert(85);
       scores.insert(90);
       scores.insert(85);
       for (const auto& score : scores) {
           std::cout << score << " ";
       }
       // 输出：85 85 90
       ```
2. 日志记录和分析：
   * 日志文件中可能包含重复的事件或消息，同时需要按照时间顺序或其他标准进行排序。`std::multiset`可以存储这些日志条目，并方便地进行查询和分析。
   *   假设存储日志的时间戳和消息内容：

       ```cpp
       struct LogEntry {
           long long timestamp;
           std::string message;
       };
       bool operator<(const LogEntry& lhs, const LogEntry& rhs) {
           return lhs.timestamp < rhs.timestamp;
       }
       std::multiset<LogEntry> logEntries;
       // 插入日志条目
       logEntries.insert({123456789, "Event 1"});
       logEntries.insert({123456790, "Event 2"});
       logEntries.insert({123456789, "Event 1 again"});
       // 可以按照时间戳顺序遍历日志
       for (const auto& entry : logEntries) {
           std::cout << entry.timestamp << ": " << entry.message << std::endl;
       }
       ```

**三、实现区间查询和范围操作**

1. 数值范围查询：
   * 当需要查询一个数值范围内的元素时，`std::multiset`可以快速返回满足条件的元素集合。例如，在一个股票价格监测系统中，可能需要查询某个价格区间内的股票。
   *   比如：

       ```cpp
       std::multiset<double> stockPrices;
       stockPrices.insert(50.5);
       stockPrices.insert(60.2);
       stockPrices.insert(55.7);
       double lowerPrice = 55.0;
       double upperPrice = 60.0;
       auto lowerIt = stockPrices.lower_bound(lowerPrice);
       auto upperIt = stockPrices.upper_bound(upperPrice);
       for (auto it = lowerIt; it!= upperIt;
       ```
