# RACSignal vs RACStream

在 ReactiveCocoa (RAC) 中，`RACSignal` 和 `RACStream` 是两个核心概念，`RACSignal` 是响应式编程中的主要工具，而 `RACStream` 则是作为流式处理的抽象基类。这两个类的关系和差异如下：

#### 1. **RACStream：数据流的抽象基类**

`RACStream` 是一个抽象基类，用于定义数据流操作的接口和规范，提供了一组通用的流式操作方法，如 `map`、`filter`、`concat` 等。`RACStream` 并不依赖于信号的实现方式，而是仅定义了如何以流的形式操作数据。

**`RACStream` 的特点**

* **抽象层级**：`RACStream` 主要用于定义流操作，提供了通用的流式操作方法（如 `map`、`filter`）。
* **通用数据操作**：可以作用于任何数据流对象，如数组、集合等。
* **不可直接使用**：作为抽象基类，不能直接实例化，需要被子类化（如 `RACSignal` 继承自 `RACStream`）。

#### 2. **RACSignal：基于事件的具体实现**

`RACSignal` 继承自 `RACStream`，实现了信号的实际行为。它不仅具备 `RACStream` 的数据流操作能力，还包括事件驱动的特性。`RACSignal` 用于处理异步事件，可以发出 `next`、`error` 和 `completed` 三种事件。

**`RACSignal` 的特点**

* **事件驱动**：`RACSignal` 是事件的载体，可以发出事件并响应状态的变化。
* **异步数据流**：它是基于异步的，适用于响应用户操作、网络请求等异步任务。
* **RACStream 的具体实现**：它继承了 `RACStream` 中定义的流式操作，如 `map` 和 `filter`，并实现了信号的管理和传递。

#### 3. **两者的关系和差异**

| 特点   | RACStream                        | RACSignal                          |
| ---- | -------------------------------- | ---------------------------------- |
| 作用   | 抽象的数据流类，定义流操作接口                  | 信号实现类，用于处理异步事件                     |
| 继承关系 | 抽象基类                             | 继承自 `RACStream`                    |
| 数据操作 | 提供通用的数据流操作方法（如 `map` 和 `filter`） | 继承了 `RACStream` 的数据操作，适用于信号        |
| 事件支持 | 不支持                              | 支持 `next`、`error` 和 `completed` 事件 |
| 使用场景 | 数据流的抽象、通用流式操作                    | 异步操作、响应式编程                         |

#### 4. **示例：`RACStream` 与 `RACSignal` 的流操作**

```objc
// 使用 RACSignal 进行操作，因为 RACSignal 继承了 RACStream 的接口
RACSignal *signal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@1];
    [subscriber sendNext:@2];
    [subscriber sendNext:@3];
    [subscriber sendCompleted];
    return nil;
}];

// 应用 RACStream 的操作方法（如 map），作用在信号上
RACSignal *mappedSignal = [signal map:^id(NSNumber *value) {
    return @(value.intValue * 2);
}];

[mappedSignal subscribeNext:^(id x) {
    NSLog(@"%@", x); // 输出: 2, 4, 6
}];
```

#### 总结

* **`RACStream`**：作为抽象基类，用于定义数据流的基本操作（如 `map`、`filter`），可扩展到多种数据类型。
* **`RACSignal`**：继承自 `RACStream`，具体实现了信号的事件驱动模型，并支持异步操作。
