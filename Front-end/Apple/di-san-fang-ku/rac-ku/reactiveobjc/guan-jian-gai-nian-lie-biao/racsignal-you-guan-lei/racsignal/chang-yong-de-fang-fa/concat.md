# concat:

在 ReactiveCocoa 中，`concat:` 方法用于将多个信号串联成一个信号，以**顺序执行**的方式依次发出每个信号的值。只有当前一个信号完成（`completed`）后，`concat:` 才会开始下一个信号。这种方法特别适用于希望严格控制多个异步任务的执行顺序的场景。

#### 基本用法

以下是 `concat:` 的使用步骤：

1. **创建多个信号**：这些信号表示一系列任务或事件。
2. **串联信号**：使用 `concat:` 将多个信号串联成一个信号。
3. **订阅串联后的信号**：订阅结果信号，将按照顺序接收到每个信号的值。

#### 示例：将多个信号串联

假设我们有两个信号 `signal1` 和 `signal2`，希望在 `signal1` 完成后再执行 `signal2`。

```objc
// 创建第一个信号
RACSignal *signal1 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"来自信号 1"];
    [subscriber sendCompleted];
    return nil;
}];

// 创建第二个信号
RACSignal *signal2 = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@"来自信号 2"];
    [subscriber sendCompleted];
    return nil;
}];

// 使用 concat 将两个信号串联
RACSignal *concatenatedSignal = [signal1 concat:signal2];

// 订阅串联后的信号
[concatenatedSignal subscribeNext:^(id x) {
    NSLog(@"接收到: %@", x);
} completed:^{
    NSLog(@"所有信号都已完成.");
}];
```

#### 输出

```
接收到: 来自信号 1
接收到: 来自信号 2
所有信号都已完成.
```

在这个例子中，`signal1` 会首先发出值 `@"来自信号 1"`，完成后 `signal2` 再发出值 `@"来自信号 2"`。

#### 注意事项

* **执行顺序**：`concat:` 按顺序依次执行每个信号，前一个信号必须完成后，才会触发下一个信号。
* **适用场景**：适用于需要串行执行的异步操作，例如网络请求、文件下载或依赖性任务。
* **与 `merge:` 区别**：`merge:` 会并行地订阅多个信号，并发地接收它们的值；而 `concat:` 是串行的，确保前一个信号完成后才开始下一个信号。

#### 高级示例：多个信号串联

假设我们有三个信号，希望将它们依次串联，并且希望每个信号都完成后才执行下一个信号：

```objc
RACSignal *signal1 = [RACSignal return:@"值 1"];
RACSignal *signal2 = [RACSignal return:@"值 2"];
RACSignal *signal3 = [RACSignal return:@"值 3"];

// 串联三个信号
RACSignal *concatenatedSignal = [[signal1 concat:signal2] concat:signal3];

// 订阅串联信号
[concatenatedSignal subscribeNext:^(id x) {
    NSLog(@"接收到: %@", x);
} completed:^{
    NSLog(@"所有信号都已完成.");
}];
```

#### 输出

```
接收到: 值 1
接收到: 值 2
接收到: 值 3
所有信号都已完成.
```

在这个例子中，每个信号会依次发出它的值，保证了严格的顺序执行。

#### 总结

* **`concat:`** 是一个串联信号的方法，用于确保按顺序执行一系列异步任务。
* 它只有在前一个信号完成后，才会开始执行下一个信号，适合需要严格执行顺序的场景。
* 可以结合多个 `concat:` 使用，创建一个多信号的顺序执行链。

`concat:` 在控制多个任务的顺序上非常有用，
