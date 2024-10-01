# Small/DenseSet

这个类是基于DenseMap来实现的 ，只不过是pair只有一个值而已，而不是key/value&#x20;



DenseSet 和 SmallDenseSet，它们都是基于密集探测哈希表的集合实现。

这些类位于 objc 命名空间中，并且使用了 LLVM 项目中的 DenseMap 和 SmallDenseMap 实现。

### 以下是代码的主要组成部分：

DenseSetEmpty 结构体这是一个空结构体，用于在 DenseMap 中作为占位符，因为 DenseSet 只关心键而不关心值。

DenseSetPair 类模板这个类模板继承自 DenseSetEmpty，并包含一个键。它是 DenseMap 中的元素类型，其中键是集合中的元素，而值是一个空的 DenseSetEmpty 实例。

DenseSetImpl 类模板这是 DenseSet 和 SmallDenseSet 的基类，它封装了一个 DenseMap 或 SmallDenseMap。它提供了集合的基本操作，如插入、删除、查找、迭代等。

DenseSet 类模板这个类模板继承自 DenseSetImpl，并使用 DenseMap 作为底层哈希表实现。它没有额外的成员或方法，只是简单地继承了基类的所有功能。

SmallDenseSet 类模板这个类模板也继承自 DenseSetImpl，但它使用 SmallDenseMap 作为底层哈希表实现。SmallDenseMap 是一个优化版本，它在内部存储了一些桶，以减少动态内存分配的开销。InlineBuckets 参数指定了内联存储的桶的数量。运算符重载代码还提供了 operator== 和 operator!= 来比较两个 DenseSetImpl 实例是否相等。注意事项

* DenseSet 和 SmallDenseSet 都使用了 DenseMapInfo 模板来提供键的哈希和比较操作。
* SmallDenseSet 通过内联存储桶来优化小集合的性能，但这也限制了它可以容纳的最大元素数量。
* 这些类模板都提供了迭代器支持，允许用户遍历集合中的元素。

这段代码是 LLVM 编译器基础设施的一部分，它提供了一个高效的方式来处理集合操作，特别是在需要频繁插入和删除元素的场景中。

其中还包括了哈希的grow和resize  放大和缩小的方法—— 哈希表变大或者变小。



### SmallDenseSet 相比 DenseSet的优势

SmallDenseSet 相比 DenseSet 的主要优势在于它使用了一种称为“内联桶”（inline buckets）的优化技术。这种技术可以在集合对象内部直接存储一些桶，而不是所有的桶都动态分配在堆上。这样做的好处包括：

1. 减少内存分配开销

：由于一部分桶是内联存储的，因此可以减少动态内存分配的次数，从而降低内存管理的开销。

2. 提高缓存局部性

：内联存储的桶更有可能在缓存中保持热状态，这可以提高访问集合元素的效率。

3. 更好的小集合性能

：对于小型的集合，内联桶可以显著提高性能，因为避免了动态内存分配和释放的开销。

4. 固定大小的内存占用

：SmallDenseSet 的内存占用在一定程度上是固定的，因为它有一部分桶是预先分配好的。这使得它在处理已知大小的小集合时更加可预测和高效。

5. 可能的初始化时间优化

：由于内联桶的存在，SmallDenseSet 在初始化时可能比 DenseSet 更快，因为它不需要立即分配动态内存。SmallDenseSet 的这些优势主要体现在处理小型集合时。当集合的大小超过内联桶的数量时，SmallDenseSet 会退回到类似于 DenseSet 的行为，此时它的性能可能会与 DenseSet 相似，因为需要动态分配额外的桶来容纳更多的元素。需要注意的是，SmallDenseSet 的内联桶数量是由模板参数 InlineBuckets 指定的，这意味着在定义 SmallDenseSet 类型时，你可以控制内联存储的桶的数量，以适应特定的使用场景。



