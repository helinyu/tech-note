# RACSignal

`RACSignal` 是 ReactiveCocoa (RAC) 框架中的一个核心概念，主要用于实现功能性响应式编程。它表示一个随时间变化的值流，允许您以声明的方式处理异步事件和数据流。以下是 `RACSignal` 的一些重要内容：

#### 核心概念

1. **信号创建**：
   * 使用 `RACSignal.createSignal:` 定义自定义信号。
   * 使用 `RACSignal.interval:` 创建一个以指定间隔发出值的信号。
   * 使用 `RACSignal.return:` 创建一个发出单个值并完成的信号。
2. **订阅**：
   * 通过 `subscribeNext:` 方法订阅信号，以接收每个发出的值。
3. **链式操作**：
   * `RACSignal` 支持链式操作，使您能够通过以下方法对信号进行转换、过滤和合并：
     * `map:`：转换发出的值。
     * `filter:`：仅允许某些值通过。
     * `merge:`：将多个信号合并为一个。
4. **错误处理**：
   * 使用 `catch:` 和 `catchError:` 方法处理信号发出的错误，从而实现优雅的错误恢复。
5. **完成**：
   * 信号可以完成，表示不会再发出更多值。可以使用 `subscribeCompleted:` 块处理完成事件。

#### 示例

以下是创建和使用 `RACSignal` 的简单示例：

```objc
// 创建一个发出值的信号
RACSignal *signal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"你好"];
    [subscriber sendNext:@"世界"];
    [subscriber sendCompleted];
    return nil; // 不需要清理
}];

// 订阅信号
[signal subscribeNext:^(id x) {
    NSLog(@"接收到: %@", x);
} completed:^{
    NSLog(@"信号完成.");
}];
```

#### 使用场景

* **网络请求**：异步处理网络请求和响应。
* **UI 事件**：以声明的方式响应用户输入（例如，按钮点击）。
* **数据绑定**：在模型和视图层之间绑定数据，实现自动更新。



