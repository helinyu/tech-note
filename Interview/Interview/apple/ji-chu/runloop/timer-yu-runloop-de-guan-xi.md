# timer 与 runloop 的关系？

`Timer` 和 `RunLoop` 之间的关系非常紧密。在 iOS 和 macOS 系统中，`NSTimer` 依赖于 `RunLoop` 来调度执行。在深入理解两者关系时，需要了解 `Timer` 的运行机制以及它是如何依靠 `RunLoop` 来管理定时任务的。

#### 1. `Timer` 的基本概念

`NSTimer` 是 iOS 中用于定时执行某段代码的工具。你可以设置一个 `Timer` 来在指定的时间间隔之后执行特定的代码块。它通常用于定时操作，比如轮询、动画更新等。

#### 2. `Timer` 和 `RunLoop` 的依赖关系

* **`NSTimer` 依赖于 `RunLoop` 运行**：`NSTimer` 需要添加到某个 `RunLoop` 中才能开始计时并触发相应的回调。`RunLoop` 会周期性地检查 `Timer` 是否到期，如果到期则会执行回调函数。
*   **`RunLoop Mode` 与 `Timer`**：`NSTimer` 运行的模式由它所在的 `RunLoop` 模式决定。不同模式下，`RunLoop` 可能只处理某些特定类型的事件。例如：

    * `NSDefaultRunLoopMode`：用于正常的事件处理（大部分场景）。
    * `UITrackingRunLoopMode`：专门处理用户交互（如滚动、触摸事件）。

    如果 `NSTimer` 被添加到一个 `RunLoop` 的 `NSDefaultRunLoopMode` 中，当 `RunLoop` 切换到其他模式时（如 `UITrackingRunLoopMode` 处理滚动事件），`NSTimer` 将停止工作，直到 `RunLoop` 切换回 `NSDefaultRunLoopMode`。

#### 3. `Timer` 的添加方式

当你创建一个 `NSTimer` 时，通常有两种方式来关联 `RunLoop`：

1.  **自动添加到 `RunLoop`**：当你使用 `scheduledTimerWithTimeInterval` 创建 `NSTimer` 时，它会自动添加到当前线程的 `RunLoop` 的默认模式 (`NSDefaultRunLoopMode`) 中。

    ```objective-c
    NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:1.0
                                                      target:self
                                                    selector:@selector(doSomething)
                                                    userInfo:nil
                                                     repeats:YES];
    ```

    这种方式不需要手动管理 `RunLoop`。
2.  **手动添加到 `RunLoop`**：如果使用 `initWithFireDate` 或 `timerWithTimeInterval` 创建 `NSTimer`，它不会自动添加到 `RunLoop` 中，必须手动调用 `addTimer:forMode:` 方法将其加入某个 `RunLoop` 中。

    ```objective-c
    NSTimer *timer = [NSTimer timerWithTimeInterval:1.0
                                             target:self
                                           selector:@selector(doSomething)
                                           userInfo:nil
                                            repeats:YES];
    [[NSRunLoop currentRunLoop] addTimer:timer forMode:NSDefaultRunLoopMode];
    ```

#### 4. `RunLoop` 的模式对 `Timer` 的影响

`RunLoop` 模式直接影响 `NSTimer` 的触发。例如，在 `UIScrollView` 滚动时，主线程的 `RunLoop` 处于 `UITrackingRunLoopMode` 模式，此时所有在 `NSDefaultRunLoopMode` 中运行的 `NSTimer` 都会暂停。当滚动结束，`RunLoop` 回到 `NSDefaultRunLoopMode` 后，`NSTimer` 才会继续触发。

如果你希望 `NSTimer` 在滚动时依然工作，可以将它添加到 `NSRunLoopCommonModes`：

```objective-c
[[NSRunLoop currentRunLoop] addTimer:timer forMode:NSRunLoopCommonModes];
```

这样 `NSTimer` 就会在所有常用模式下都继续工作，包括 `NSDefaultRunLoopMode` 和 `UITrackingRunLoopMode`。

#### 5. `Timer` 和 `RunLoop` 的调度原理

* `RunLoop` 是一个事件循环，每次循环时会检查它管理的所有输入源（如事件、端口、定时器）是否有任务需要处理。
* `NSTimer` 被添加到 `RunLoop` 后，`RunLoop` 会在每次循环时检查该定时器是否已经到期。如果到期了，就会执行 `NSTimer` 的回调。
* 如果当前 `RunLoop` 处于休眠状态（等待输入源或定时器触发），`NSTimer` 到期后会唤醒 `RunLoop`，从而让定时器回调得以执行。

#### 6. `Timer` 和线程的关系

* **主线程上的 `Timer`**：主线程的 `RunLoop` 是默认运行的，因此在主线程中使用 `NSTimer` 是很常见的。`NSTimer` 会自动加入到主线程的 `RunLoop`，确保 UI 能及时响应。
* **子线程上的 `Timer`**：子线程默认没有 `RunLoop`，如果需要在子线程中使用 `NSTimer`，必须手动创建并启动该线程的 `RunLoop`。否则，`NSTimer` 不会触发。

在子线程中运行 `Timer` 的示例：

```objective-c
[NSThread detachNewThreadSelector:@selector(startTimerInThread) toTarget:self withObject:nil];

- (void)startTimerInThread {
    @autoreleasepool {
        // 启动 RunLoop 使得线程不会在任务结束后退出
        NSTimer *timer = [NSTimer timerWithTimeInterval:1.0 target:self selector:@selector(doSomething) userInfo:nil repeats:YES];
        [[NSRunLoop currentRunLoop] addTimer:timer forMode:NSDefaultRunLoopMode];
        [[NSRunLoop currentRunLoop] run];  // 启动 RunLoop
    }
}
```

#### 7. `Timer` 的注意事项

* **精度问题**：`NSTimer` 的时间并不是精确的，它的执行时间依赖于 `RunLoop` 的状态。如果 `RunLoop` 在处理其他高优先级任务时，`NSTimer` 可能会延迟执行。
* **与 `RunLoop` 休眠的关系**：如果 `RunLoop` 进入了休眠状态，`NSTimer` 需要等到 `RunLoop` 被唤醒才会执行。这意味着 `NSTimer` 的实际触发时间可能会受到影响。

#### 总结

* `NSTimer` 是依赖 `RunLoop` 运行的定时工具。没有 `RunLoop`，`NSTimer` 将无法正常工作。
* `RunLoop` 决定了 `NSTimer` 何时执行，并通过不同的 `RunLoop` 模式来控制 `NSTimer` 的调度和运行。
* 在使用 `NSTimer` 时需要了解 `RunLoop` 的模式切换，确保定时器能在需要的场景中正常工作（如滚动视图时 `NSTimer` 的暂停与恢复）。
