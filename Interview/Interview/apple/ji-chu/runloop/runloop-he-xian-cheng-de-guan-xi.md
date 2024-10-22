# runloop和线程的关系？

`RunLoop` 和线程之间的关系非常密切，但两者是不同的概念。<mark style="color:red;">`RunLoop`</mark> <mark style="color:red;"></mark><mark style="color:red;">是线程的一部分，负责管理线程的生命周期和事件循环</mark>。每个线程都可以拥有一个 `RunLoop`，但并不是所有的线程都会自动创建 `RunLoop`，主线程是系统自动为其创建并运行 `RunLoop` 的，而子线程需要手动启动 `RunLoop`。

#### 1. 线程与 `RunLoop` 的基本关系

* **每个线程都有一个唯一的 `RunLoop`**：每个线程都有一个对应的 `RunLoop` 实例，`RunLoop` 是基于线程的。主线程的 `RunLoop` 在应用程序启动时就被系统创建并自动启动，而子线程的 `RunLoop` 则需要开发者手动创建并启动。
* **`RunLoop` 与线程的绑定**：`RunLoop` 是与线程绑定的，也就是说一个 `RunLoop` 只能运行在创建它的那个线程中，不能跨线程访问或操作其他线程的 `RunLoop`。
* **主线程的 `RunLoop`**：主线程（即 UI 线程）是应用程序的核心，负责处理用户交互、UI 更新和其他系统事件。主线程的 `RunLoop` 保证应用程序能够持续运行并响应各种事件。
* **子线程的 `RunLoop`**：子线程不会自动创建 `RunLoop`。如果在子线程中需要处理定时器、输入源事件等，就需要手动启动该线程的 `RunLoop`。

#### 2. `RunLoop` 在线程中的作用

* **线程的存活与 `RunLoop`**：线程的生命周期与 `RunLoop` 的运行状态密切相关。主线程通过 `RunLoop` 来保持活跃状态，保证应用在运行时可以持续响应用户操作。对于子线程，如果没有 `RunLoop`，线程执行完任务后会自动退出；通过运行 `RunLoop`，子线程可以保持活跃，等待处理新的事件或任务。
* **管理事件循环**：`RunLoop` 使线程能够在不执行任务时进入休眠状态，并在有新事件（如定时器、输入源等）时被唤醒进行处理。它通过高效的事件循环来避免线程长期占用 CPU 资源。
* **处理异步任务**：`RunLoop` 可以监听异步任务的结果，例如网络请求的回调、定时器的触发等。这样可以避免阻塞线程，尤其是主线程上的操作。

#### 3. 主线程和 `RunLoop`

主线程是 iOS 应用的核心线程，所有 UI 操作都必须在主线程上执行。主线程的 `RunLoop` 会自动启动，负责：

* 处理 UI 事件，如触摸、按钮点击。
* 响应定时器和动画更新。
* 处理网络请求的回调或通知。

#### 4. 子线程和 `RunLoop`

默认情况下，子线程不启用 `RunLoop`，因为它们通常用于执行短暂的后台任务，完成后就会自动退出。但是，在以下情况中，子线程可能需要 `RunLoop`：

* 需要在子线程中处理异步事件（如网络请求、文件 I/O）。
* 使用 `NSTimer` 或者其他需要长时间运行的操作。
* 想让线程保持活跃而不是执行完后立即退出。

要在子线程中使用 `RunLoop`，需要手动调用如下代码：

```objective-c
// 获取当前线程的 RunLoop
NSRunLoop *runLoop = [NSRunLoop currentRunLoop];

// 添加一个输入源或定时器，以保持 RunLoop 活跃
[NSTimer scheduledTimerWithTimeInterval:1.0
                                 target:self
                               selector:@selector(doSomething)
                               userInfo:nil
                                repeats:YES];

// 启动 RunLoop
[runLoop run];
```

#### 5. `RunLoop` 和线程的特点

* **主线程必须有 `RunLoop`**：没有 `RunLoop`，应用无法响应用户交互，主线程会在应用启动时自动进入 `RunLoop`，以便不断监听和处理事件。
* **子线程的 `RunLoop` 是可选的**：子线程可以手动启动 `RunLoop`，但如果子线程只用来执行短暂的任务，就不需要 `RunLoop`。但是，如果子线程需要处理长时间的异步任务或等待事件触发，那么需要运行 `RunLoop` 来保持线程活跃。

#### 6. `RunLoop` 和线程的局限

* **`RunLoop` 不能跨线程共享**：一个线程的 `RunLoop` 只能用于该线程自身，不能在其他线程中使用或操作。
* **性能考虑**：在主线程中运行复杂的长时间任务会阻塞 `RunLoop`，导致应用卡顿。因此，长时间任务应该放到后台线程中执行，并通过 `RunLoop` 进行异步处理。

#### 总结

`RunLoop` 是线程的事件循环机制，主线程自动运行 `RunLoop` 来处理 UI 事件，而子线程需要手动启动 `RunLoop` 来管理异步事件和保持线程活跃。通过 `RunLoop`，线程可以在没有任务时休眠，节省系统资源，同时在需要时唤醒并处理事件。
