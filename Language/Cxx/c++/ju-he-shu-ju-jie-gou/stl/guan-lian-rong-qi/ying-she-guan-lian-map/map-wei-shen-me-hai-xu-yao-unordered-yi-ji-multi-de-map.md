# map 为什么还需要unordered 以及multi的map？



**一、unordered**&#x20;

1. 底层数据结构和性能特点：
   * `std::map`：底层通常是<mark style="color:red;">**红黑树**</mark>实现。它保证了元素的有序性，即按照键的特定顺序进行存储和遍历。插入、删除和查找操作的时间复杂度为 $O(log n)$，其中 `n` 是容器中的元素数量。
   * `std::unordered_map`：底层是<mark style="color:red;">**哈希表**</mark>实现。在平均情况下，插入、删除和查找操作的时间复杂度接近常量时间 $O(1)$，但在最坏情况下可能会退化为 $O(n)$<mark style="color:orange;">。如果对性能要求较高，尤其是在不需要严格有序存储的情况下，</mark><mark style="color:orange;">`unordered_map`</mark> <mark style="color:orange;"></mark><mark style="color:orange;">可能更适合。</mark>
2. 适用场景：
   * 当需要按照键的**特定顺序遍历元素，或者需要支持范围查询等操作时**，`std::map` 是更好的选择。例如，按字典序遍历单词及其出现次数的场景。
   * 当更注重快速的插入、删除和查找操作，而<mark style="color:orange;">**不关心元素的顺序时**</mark>，`std::unordered_map` 更为合适。比如存储大量用户 ID 和用户信息，且不需要按照特定顺序访问这些信息的场景。

**二、`multi` 的存在必要性**

1. 支持多值映射：
   * `std::map` 和 `std::unordered_map` 都是一对一的映射关系，即一个键只能对应一个值。而 <mark style="color:red;">**`multi`**</mark><mark style="color:red;">** **</mark><mark style="color:red;">**允许一个键对应多个值，可以存储重复的键值对**</mark>。
   * 例如，<mark style="color:orange;">**在统计文本中每个单词出现的位置时，一个单词可能在多个位置出现**</mark>，这时使用 `multi` 可以方便地存储单词和其对应的多个位置信息。
2. 灵活性：
   * 在某些情况下，可能无法预先确定一个键是否会重复出现，或者需要动态地添加多个具有相同键的值。`multi` 提供了这种灵活性，不需要进行复杂的逻辑处理来处理重复键的情况。

<mark style="color:red;">**提供了更多的选择和灵活性。**</mark>



## 总结：

1、唯一性

2、有序性

3、多键值

