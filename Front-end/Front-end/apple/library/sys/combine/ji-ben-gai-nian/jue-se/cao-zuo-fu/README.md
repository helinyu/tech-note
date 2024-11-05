# 操作符

在 Combine 框架中，操作符（Operators）用于处理和变换发布者（Publishers）发出的值。常见的操作符可以按功能分为几类，以下是一些主要类型的操作符：

#### 1. **创建发布者（Creating Publishers）**

* [`Just`](../fa-bu-zhe/just/): 创建一个只发布单一值的发布者。
* [`Future`](../fa-bu-zhe/future.md): 创建一个异步操作的发布者，发布一个未来的值。
* [`Deferred`](../fa-bu-zhe/deferred.md): 延迟创建发布者，直到订阅时才生成。

#### 2. **变换操作符（Transformation Operators）**

* [`map`](map/): 转换发布者发出的值。
* [`compactMap`](map/map-trymap-compactmap-flatmap.md): 转换发布者发出的值，忽略 `nil` 值。
* [`flatMap`](map/flatmap.md): 将每个发布的值映射为一个新的发布者。
* [`tryMap`](map/map-trymap-compactmap-flatmap.md): 对发布的值进行转换，并捕获错误。
* [`scan`](scan.md): 累积每个发布的值。
* [reduce](reduce.md) 多个值合并为一个单一的值

#### 3. **过滤操作符（Filtering Operators）**

* [`filter`](filter.md): 过滤发布者发出的值，保留符合条件的值。
* `tryFilter`: 对发布的值进行条件判断，并捕获错误。 类似map中的trymap
* [`removeDuplicates`](removeduplicates/): 移除<mark style="color:red;">连续相同</mark>的值。
* [`ignoreOutput`](ignoreoutput.md): 忽略发布者发出的所有值，仅关心完成或失败事件。



#### 4. [**合并和组合**](vs/mergezipcombinelatest-he-switchtolatest.md)**操作符（Combining and Merging Operators）**

* [`merge`](merge.md): 将多个发布者合并为一个。
* [`combineLatest`](combinelatest.md): 等待多个发布者都发出一个值时，合并这些值。
* [`zip`](zip.md): 将两个发布者的输出按顺序配对。
* [`switchToLatest`](switchtolatest.md): 订阅一个发布者，并且当其发出新的发布者时切换订阅到新发布者。

#### 5. **调度和延迟操作符（Timing and Scheduling Operators）**

* [`delay`](delay.md): 延迟发布者的输出。
* [`debounce`](debounce.md): 等待发布者发出一段时间没有新的值后，再发出最后的值。
* [`throttle`](throttle.md): 在一段时间内只允许发布一次值。
* `timeout`: 为发布者设置超时时间。

#### 6. **订阅操作符（Subscription Operators）**

* [`sink`](../jie-shou-zhe/sink.md): 最常用的订阅操作符，定义当发布者发送值时的回调。
* [`assign`](../jie-shou-zhe/assign.md): 将发布的值直接赋值给某个属性。

#### 7. [**错误处理操作符（Error Handling Operators）**](vs/catch-trycatch-retry-tryretry.md)

* `catch`: 捕获并处理发布者的错误。
* `tryCatch`: 捕获并处理错误，但允许抛出错误。
* `retry`: 在失败后尝试重新订阅发布者。
* `tryRetry`: 尝试重新订阅并捕获错误。

#### 8. [**调试操作符（Debugging Operators）**](tiao-shi-printhandleevents.md)

* `print`: 打印发布者发出的值和事件。
* `handleEvents`: 在发布者的生命周期中捕获并处理事件（如订阅、接收值、完成或失败）。

9. [共享数据流](share-muticast.md)

* share: 多个订阅者订阅同一个数据流
* multicast: 更精细控制的场景

