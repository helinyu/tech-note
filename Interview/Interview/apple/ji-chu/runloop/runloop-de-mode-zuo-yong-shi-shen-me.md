# Runloop的mode作用是什么？

`RunLoop` 的模式（mode）是用于控制和管理事件处理的机制。通过设置不同的 `RunLoop` 模式，你可以决定在特定情况下 `RunLoop` 如何响应事件、处理输入源、以及触发定时器等。以下是 `RunLoop` 模式的主要作用和相关概念：

#### 1. **事件处理的控制**

每个 `RunLoop` 模式定义了一组输入源和定时器，当 `RunLoop` 运行在某个特定模式下时，只有该模式中注册的输入源和定时器会被激活和处理。这使得应用程序可以根据不同的上下文管理事件响应。

#### 2. **常用模式**

* **`kCFRunLoopDefaultMode`**：默认模式，通常用于大多数情况。当 `RunLoop` 处于此模式时，会处理用户交互、定时器和其他输入源。
* **`UITrackingRunLoopMode`**：用于处理 UI 交互事件，如滚动、拖动等。当 `RunLoop` 处于此模式时，可能会优先处理这些事件，忽略其他类型的输入源。
* **`kCFRunLoopCommonModes`**：一个特殊的模式集合，允许多个模式共享相同的输入源。可以将某些输入源注册到 `kCFRunLoopCommonModes`，使它们在多个模式下有效。

#### 3. **多模式使用场景**

通过使用不同的模式，可以更精确地控制应用程序在特定情况下的响应行为。以下是一些使用场景：

* **UI 切换**：当用户与界面交互时，你可能希望 `RunLoop` 只处理与用户交互相关的事件，因此使用 `UITrackingRunLoopMode`。
* **后台任务**：在执行某些后台任务时，可能希望将 `RunLoop` 切换到一个自定义模式，以处理相关的输入源和定时器。
* **定时器的有效性**：如果你在特定模式下注册了定时器，只有在切换到该模式时，定时器才会被激活和触发。

#### 4. **模式切换的影响**

* 当 `RunLoop` 切换模式时，会停止处理当前模式中的输入源，并开始处理新模式中的输入源。只有在新模式下注册的定时器和输入源会生效。
* `RunLoop` 可以通过调用 `CFRunLoopRunInMode` 方法显式地运行于特定模式，允许开发者根据需要控制 `RunLoop` 的行为。

#### 5. **模式的注册**

你可以将输入源、定时器和观察器注册到特定的模式。例如，以下代码展示了如何在 `kCFRunLoopCommonModes` 模式中注册定时器：

```objective-c
// 创建一个 NSTimer，每 3 秒执行一次某个方法
NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:3.0
                                                  target:self
                                                selector:@selector(timerFired:)
                                                userInfo:nil
                                                 repeats:YES];

// 将 NSTimer 添加到 kCFRunLoopCommonModes 模式
[[NSRunLoop currentRunLoop] addTimer:timer forMode:NSRunLoopCommonModes];
```

#### 6. **总结**

`RunLoop` 的模式是事件管理的重要机制，允许你根据不同的上下文和需求控制事件的响应行为。通过使用不同的模式，你可以灵活地管理输入源、定时器和观察器的激活与处理，从而实现高效且响应灵敏的应用程序。
