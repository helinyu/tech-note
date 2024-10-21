# 程序中添加每3秒响应一次的NSTimer，当拖动tableview时timer可能无法响应要怎么解决？

当你在拖动 `UITableView` 或其他类似视图时，主线程的 `RunLoop` 会切换到 `UITrackingRunLoopMode`，这会导致在 `NSDefaultRunLoopMode` 中运行的 `NSTimer` 停止响应。因此，`NSTimer` 无法在拖动期间触发。

要解决这个问题，你可以将 `NSTimer` 添加到 `NSRunLoopCommonModes`，这样 `NSTimer` 就能够在所有常用的 `RunLoop` 模式下运行，包括 `UITrackingRunLoopMode`，从而保证在拖动 `UITableView` 时也能继续响应。

#### 解决方案

下面的示例展示了如何将 `NSTimer` 添加到 `NSRunLoopCommonModes`，以确保在 `UITableView` 滚动时，定时器仍然能够每 3 秒触发一次。

```objective-c
NSTimer *timer = [NSTimer timerWithTimeInterval:3.0
                                          target:self
                                        selector:@selector(timerFired)
                                        userInfo:nil
                                         repeats:YES];

// 将 timer 添加到 NSRunLoopCommonModes，确保在所有常用模式下都能触发
[[NSRunLoop currentRunLoop] addTimer:timer forMode:NSRunLoopCommonModes];
```

#### 解释

* **`NSTimer timerWithTimeInterval`**：创建一个 `NSTimer` 对象，每 3 秒触发一次回调。
* **`addTimer:forMode:`**：将 `NSTimer` 添加到 `RunLoop` 的 `NSRunLoopCommonModes` 模式中。`NSRunLoopCommonModes` 包含了多个 `RunLoop` 模式，如 `NSDefaultRunLoopMode` 和 `UITrackingRunLoopMode`，确保定时器在正常运行和滚动视图交互时都能继续运行。

#### 常见的 `RunLoop` 模式

* `NSDefaultRunLoopMode`：主线程正常运行时的默认模式。
* `UITrackingRunLoopMode`：当用户进行 UI 交互（如滚动 `UITableView`）时的模式。
* `NSRunLoopCommonModes`：是一个占位符模式，包含多个 `RunLoop` 模式。把 `NSTimer` 添加到 `NSRunLoopCommonModes`，可以让它在多个模式下工作，包括 `NSDefaultRunLoopMode` 和 `UITrackingRunLoopMode`。

#### 总结

将 `NSTimer` 添加到 `NSRunLoopCommonModes` 是解决在 `UITableView` 滚动时定时器停止响应的有效方法。这样，无论在默认模式下，还是在拖动 `UITableView` 进入 `UITrackingRunLoopMode` 时，定时器都能正常触发每 3 秒的回调。
