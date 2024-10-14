# 头文件定义



#### **这几个方法需要子类去重写的**

* **创建空流**：`+ (RACStream *)empty;`
* **将单个值转换为流**：`+ (RACStream *)return:(id)value;`
* **绑定值到块**：`- (RACStream *)bind:(RACStreamBindBlock (^)(void))block;` 允许早期终止或闭包状态
* **连接流**：`- (RACStream *)concat:(RACStream *)stream;` 连接两个相同类型的流
* **打包流**：`- (RACStream *)zipWith:(RACStream *)stream;` 将多个流中的值组合成元组



* **映射和扁平化**：`- (RACStream *)flattenMap:(RACStream * (^)(id value))block;` 应用于每个值并<mark style="color:red;">**合并结果流**</mark>
* `flatten`：将嵌套的数据流扁平化为单一数据流，并保留原始数据流的名字。
* `map`：对数据流中的每个值应用转换块（block），并设置转换后的新数据流名称。其中`block`参数不能为空。
* mapReplace 收一个对象`object`作为参数，并返回一个新的RACStream
* **过滤**：`- (RACStream *)filter:(BOOL (^)(id value))block;` 过滤不符合条件的值
* **忽略特定值**：-ignore: 接收一个参数 `value`，并返回一个新的 `RACStream` 对象。
* `startWith:`：此函数接收一个值，并创建一个新的流，在原有流开始前先发出这个值。
* **跳过值**：`- (RACStream *)skip:(NSUInteger)skipCount;` 跳过指定数量的初始值
* **取前N个值**：`- (RACStream *)take:(NSUInteger)count;` 取指定数量的初始值
* combinePreviousWithStart:reduce: 用于创建一个新的数据流，该流中的每个元素都是基于初始值`start`和前一个元素计算得出的结果。
* `join:`函数：将多个流组合成一个流，每个值被包装成元组。首次迭代时，将第一个流的值包装为单元素元组；后续迭代调用`block`方法组合当前流和新加入的流。
* `zip:`函数：通过`join:`函数实现对多个流的逐元素组合，并返回一个新的流。
* `zip:reduce:`函数：与`zip:`类似，但额外应用一个reduce操作来处理组合后的元素，最终生成新的流。
* `concat:`函数：将多个流依次连接成一个连续的流。
* **归约**：`- (RACStream *)reduceEach:(RACReduceBlock)reduceBlock;` 对每个元组值进行归约处理
* **扫描**：`- (RACStream *)scanWithStart:(id)startingValue reduce:(id (^)(id running, id next))reduceBlock;` 从左至右结合值生成新流
* `scanWithStart:reduceWithIndex:`：同样接收初始值和累积块，但累积块还接收当前元素索引，并返回处理后的新流。内部通过`bind`方法实现累积操作，并更新累积值和索引。
* `takeUntilBlock:`：返回一个新的流，该流会持续传递值直到`predicate`首次为真。
* `takeWhileBlock:`：通过取反`predicate`调用`takeUntilBlock:`来实现，返回一个流，当`predicate`为真时继续传递值。
* `skipUntilBlock:`：返回一个新的流，在`predicate`首次为真之前忽略所有值。
* `skipWhileBlock:`：通过取反`predicate`调用`skipUntilBlock:`来实现，返回一个流，在`predicate`为假之前忽略所有值。
* `distinctUntilChanged`：返回一个新的流，只在值发生变化时传递，相同值会被过滤掉。

\
