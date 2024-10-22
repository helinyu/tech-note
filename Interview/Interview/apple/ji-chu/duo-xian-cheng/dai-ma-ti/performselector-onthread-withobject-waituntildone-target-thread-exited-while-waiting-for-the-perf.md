# performSelector:onThread:withObject:waitUntilDone:]: target thread exited while waiting for the perf

这个错误信息表明，`performSelector:onThread:withObject:waitUntilDone:modes:` 方法在目标线程退出时试图执行选择器（selector）。这是一个常见的多线程问题，尤其是在使用 `performSelector` 进行线程间通信时。

#### 可能的原因

1. **目标线程已退出**：你可能在一个已经结束的线程上调用了 `performSelector`，导致抛出 `NSDestinationInvalidException` 异常。
2. **选择器未找到**：在目标线程上找不到对应的选择器或对象。
3. **线程同步问题**：在某些情况下，如果多个线程竞争资源，可能导致意外的线程结束或状态不一致。

#### 解决方案

1. **检查线程状态**：在调用 `performSelector` 之前，确保目标线程仍然处于活动状态。可以通过检查线程是否已终止来确保安全。
2. **使用合适的线程管理**：考虑使用 `NSThread`、`GCD` 或 `NSOperationQueue` 来管理线程。可以避免直接操作线程的生命周期。
3.  **使用 `dispatch_async`**：如果你使用的是 GCD，建议使用 `dispatch_async` 来替代 `performSelector:onThread:`，例如：

    ```objc
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        // 执行你的任务
    });
    ```
4. **确保选择器的存在**：在目标线程中确保选择器对应的方法存在，并且能被正确调用。
5. **调试与日志**：在代码中加入适当的日志输出，跟踪线程的创建和结束，以便更好地了解问题发生的上下文。

#### 示例代码

如果你在使用 `performSelector:onThread:withObject:waitUntilDone:modes:`，可以考虑以下的改写示例：

```objc
// 创建并启动一个线程
NSThread *myThread = [[NSThread alloc] initWithTarget:self selector:@selector(myThreadMethod) object:nil];
[myThread start];

// 使用 GCD 替代
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    [self myThreadMethod];
});

// 定义选择器方法
- (void)myThreadMethod {
    @autoreleasepool {
        // 线程执行的任务
        NSLog(@"Running on thread: %@", [NSThread currentThread]);
    }
}
```

#### 总结

要解决 `'NSDestinationInvalidException'`，确保在调用选择器时目标线程仍处于活动状态，并考虑使用更现代的多线程编程模式，如 GCD 或 NSOperationQueue。这样可以更好地管理线程的生命周期，减少潜在的错误。
