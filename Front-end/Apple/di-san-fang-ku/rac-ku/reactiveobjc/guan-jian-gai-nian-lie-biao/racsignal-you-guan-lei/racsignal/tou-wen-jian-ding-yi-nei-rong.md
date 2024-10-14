# 头文件定义内容



### 有关方法：

定义了`RACSignal`类，继承自`RACStream`，提供了创建和操作异步事件流的方法：

1. **信号创建**：提供多种静态方法创建信号，如`createSignal:`允许自定义事件发送逻辑；`error:`、`never`等用于创建预定义行为的信号。

<pre class="language-cpp" data-overflow="wrap"><code class="lang-cpp">+createSignal： 创建信号 , 允许在block里面自定义事件发送逻辑。
+error：返回一个RACSignal对象。该信号会立即发送给定的错误（NSError）。如果error参数为nil，则可能返回一个无效的信号。建议将返回值用于进一步的错误处理。
+never  返回一个永远不会完成的RACSignal对象。主要功能：<a data-footnote-ref href="#user-content-fn-1">创建一个不会结束的信号，通常用于需要无限运行的场景</a>。

+ (RACSignal&#x3C;ValueType> *)startEagerlyWithScheduler:(RACScheduler *)scheduler block:(void (^)(id&#x3C;RACSubscriber> subscriber))block; 这个方法还灭有用到，暂时还不理解
+ (RACSignal&#x3C;ValueType> *)startLazilyWithScheduler:(RACScheduler *)scheduler block:(void (^)(id&#x3C;RACSubscriber> subscriber))block RAC_WARN_UNUSED_RESULT;

1、startEagerlyWithScheduler:...: 在第一次订阅时立即执行给定的block，并将事件发送给订阅者。无论后续有多少订阅者，block只执行一次。
2、startLazilyWithScheduler:...: 与startEagerlyWithScheduler:...类似，但在每次新订阅时都会重新执行block，并将事件发送给当前订阅者，确保每个订阅者都从头开始接收事件。
两者均接受调度器和发送事件的block作为参数。注意，返回的信号不会自动取消底层订阅。
</code></pre>

2. **和流有关的方法**

**`1）return:`**

* 返回一个信号，该信号会立即发送给定的值（`value`）并完成。
* 用于创建一个简单的信号，仅包含一个值。

**`2）empty`**

* 返回一个空信号，该信号会立即完成而不发送任何值。
* 用于表示没有数据传输的信号。

**`3）`typedef RACSignal \* \_Nullable (^RACSignalBindBlock)(ValueType \_Nullable value, BOOL \*stop);**

定义的一个block类型，用于下面的bind

* 定义了一个类型别名，表示一个接收值并返回新信号的块。
* 块参数：
  * `value`: 可能为 `null` 的值类型。
  * `stop`: 一个布尔值指针，设置为 `YES` 表示终止绑定；`NO` 则继续。
* 返回值：可为 `null` 的信号。

**`4）`**[**(RACSignal \*)bind:(RACSignalBindBlock (^)(void))block** ](chang-yong-de-fang-fa/bind.md)

* 懒惰地将一个块绑定到接收器中的值。
* 适用于需要提前终止绑定或闭包状态的情况。
* 参数：
  * `block`: 一个返回 `RACSignalBindBlock` 的块，每次重新评估绑定信号时调用。
* 要求：该块不能为 `nil` 或返回 `nil`。
* 返回值：一个新的信号，代表所有懒惰应用 `block` 的组合结果。

**`5）`**[**`concat`**](chang-yong-de-fang-fa/concat.md)**`:`**

* 当源信号完成后，订阅另一个信号。
* 参数：
  * `signal`: 需要连接的信号，不能为 `nil`。
* 返回值：一个新的信号，依次发送两个信号的所有值。

**`6）`**[**`zipWith`**](chang-yong-de-fang-fa/zipwith-he-merge.md)**`:`**

* 将接收器中的值与另一个信号中的值组合成 `RACTuple`。
* 参数：
  * `signal`: 需要组合的信号，不能为 `nil`。
* 组合方式：第一个 `next` 值组合，然后第二个 `next` 值组合，以此类推，直到其中一个信号完成或出错。
* 返回值：一个新的信号，包含组合后的 `RACTuple` 值。如果任一原始信号出错，则错误会在返回的新信号中转发。



3. **操作符**：包括`flattenMap:`（映射并展平）、`flatten`（合并信号）、`map:`（映射值）、`filter:`（过滤值）等常见操作符来转换或筛选信号中的数据。



1. **flattenMap**: 将接收器中的值通过`block`转换为新的信号，并将结果信号合并成一个新信号。
2. **flatten**: 合并信号中的信号为单一信号。
3. **map**: 将接收器中的每个值通过`block`进行转换。
4. **mapReplace**: 用给定对象替换接收器中的每个值。
5. **filter**: 过滤掉不满足`block`条件的值。
6. **ignore**: 过滤掉与给定值相等的值。
7. **reduceEach**: 解包接收器中的每个RACTuple并通过`reduceBlock`映射值。
8. **startWith**: 返回一个新的信号，该信号以给定值开始，然后是接收器中的值。
9. **skip**: 跳过接收器中的前`skipCount`个值。
10. **take**: 取接收器中的前`count`个值。
11. **zip**: 将多个信号的值组合成RACTuple。
12. **zip...reduce**: 将信号组合后通过`reduceBlock`减少为单个值。
13. **concat**: 按顺序连接多个信号。
14. **scanWithStart...reduce**: 使用`reduceBlock`从左到右累积接收器中的值。
15. **scanWithStart...reduceWithIndex**: 类似于`scanWithStart...reduce`，但包含值的索引。
16. **combinePreviousWithStart...reduce**: 结合前一个和当前值。
17. **takeUntilBlock**: 取值直到`predicate`返回`YES`。
18. **takeWhileBlock**: 取值直到`predicate`返回`NO`。
19. **skipUntilBlock**: 跳过值直到`predicate`返回`YES`。
20. **skipWhileBlock**: 跳过值直到`predicate`返回`NO`。
21. **distinctUntilChanged**: 返回与前一值不同的值。



4. **订阅管理**：通过`subscribe:`及其变体方法支持不同场景下的信号订阅与取消订阅。

* `subscribe:`
  * 订阅事件，参数为订阅者对象。
* `subscribeNext:`
  * 订阅 `next` 事件，参数为处理 `next` 事件的 block。
* `subscribeNext:completed:`
  * 订阅 `next` 和 `completed` 事件，参数分别为处理 `next` 和 `completed` 事件的 block。
* `subscribeNext:error:completed:`
  * 订阅 `next`、`error` 和 `completed` 事件，参数分别为处理这三种事件的 block。
* `subscribeError:`
  * 订阅 `error` 事件，参数为处理 `error` 事件的 block。
* `subscribeCompleted:`
  * 订阅 `completed` 事件，参数为处理 `completed` 事件的 block。
* `subscribeNext:error:`
  * 订阅 `next` 和 `error` 事件，参数分别为处理这两种事件的 block。
* `subscribeError:completed:`
  * 订阅 `error` 和 `completed` 事件，参数分别为处理这两种事件的 block。



5. **调试工具**：如`logAll`、`logNext`等方法帮助开发者调试信号的行为。
6. **单元测试辅助**：提供了`asynchronousFirstOrDefault:`、`asynchronouslyWaitUntilCompleted:`等方法，仅用于单元测试环境中验证信号的行为。

[^1]: 
