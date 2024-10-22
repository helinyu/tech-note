# Runloop内部实现逻辑？

`RunLoop` 的内部实现逻辑相当复杂，但其核心思想可以归结为一个事件循环（Event Loop）的管理机制。具体来说，`RunLoop` 负责在一个循环中监听输入源，处理定时器、事件和回调，休眠直到下一个事件到来。这里是 `RunLoop` 内部实现的关键步骤和流程：

#### 1. `RunLoop` 的基本结构

`RunLoop` 是一个线程的基础设施，每个线程都有一个唯一的 `RunLoop`，但它不会自动创建，必须在首次访问时手动获取或创建。主线程的 `RunLoop` 是系统自动创建并运行的，而子线程则需要手动启动。

* **输入源（Input Sources）**：用于处理异步事件。分为两种：
  * **Port-based sources**：如 `NSPort`、`mach_port`，用于与其他线程或进程通信。
  * **Custom input sources**：自定义输入源，可以将自定义事件添加到 `RunLoop` 中处理。
* **定时源（Timer Sources）**：用于处理时间相关的任务，`NSTimer` 和 `CADisplayLink` 就是基于 `RunLoop` 的定时源。
* **Observer（观察者）**：用于监听 `RunLoop` 的状态变化，例如 `RunLoop` 进入、退出、即将休眠等。

#### 2. `RunLoop` 的基本执行流程

`RunLoop` 的内部执行流程可以概括为以下几步：

1. **通知观察者即将进入 `RunLoop`**：`RunLoop` 启动时，会先通知所有注册的 `CFRunLoopObserver` 对象，即 `RunLoop` 处于即将进入状态。观察者可以通过这个时机执行一些初始化操作。
2. **检查输入源和定时器**：`RunLoop` 会检查当前线程是否有需要处理的输入源事件或定时器。如果有，进入处理流程。
3. **通知观察者即将处理 `RunLoop` 事件**：`RunLoop` 在处理事件之前会再一次通知观察者，告诉他们将要开始处理事件。
4. **处理输入源事件或定时器回调**：如果有输入源事件或定时器到期，`RunLoop` 会调用相应的处理程序执行任务。例如，用户触摸事件会通过 `UIKit` 中的输入源传递到 `RunLoop`，然后由 `RunLoop` 分发到应用的回调函数。
5. **通知观察者即将进入休眠**：当没有事件需要处理时，`RunLoop` 会通知观察者它即将进入休眠状态。
6. **进入休眠**：如果没有需要处理的事件或定时任务，`RunLoop` 会进入休眠状态，直到有新的事件发生或者定时器触发时才被唤醒。
7. **唤醒 `RunLoop`**：`RunLoop` 由外部事件或定时器唤醒，进入下一次事件循环，返回到步骤 2。
8. **通知观察者即将退出 `RunLoop`**：当 `RunLoop` 退出时（例如线程终止或手动调用 `stop`），会通知观察者，让它们可以执行清理操作。

#### 3. `RunLoop` 的具体实现机制

`RunLoop` 的底层实现依赖于 **`CFRunLoop`**，这是 Core Foundation 层的 C 接口，与 `NSRunLoop` 是一一对应的。`CFRunLoop` 的核心机制是基于系统的低级事件处理 API，如 `mach port`、`select()` 或 `poll()` 系统调用，用于监听和分发各种事件。

* **Mode 模式**：`RunLoop` 可以运行在不同的模式下，每个模式会监控特定的输入源和定时器。常见模式包括 `NSDefaultRunLoopMode` 和 `UITrackingRunLoopMode`。通过使用不同的模式，`RunLoop` 可以避免在某些情况下（如滚动视图时）被不必要的事件打断。
* **事件循环机制**：`RunLoop` 的事件循环通过一个 `while` 循环不断重复执行，只要 `RunLoop` 被启动且未被终止，它将会一直运行，直到手动停止。事件循环是高效的，因为它会在没有事件时休眠，从而节省 CPU 资源。

```c
while (runLoopIsRunning) {
    // 通知观察者即将进入
    notifyObservers(kCFRunLoopEntry);
    
    // 处理事件源和定时器
    handleSourcesAndTimers();
    
    // 通知观察者即将休眠
    notifyObservers(kCFRunLoopBeforeWaiting);
    
    // 进入休眠，等待事件唤醒
    sleepUntilEvent();
    
    // 事件到达后唤醒，通知观察者
    notifyObservers(kCFRunLoopAfterWaiting);
    
    // 如果需要退出，跳出循环
    if (shouldExit) break;
    
    // 继续循环
}
```

#### 4. 线程与 `RunLoop`

* **主线程**：主线程的 `RunLoop` 是自动创建并运行的，它确保应用的 UI 不断响应用户操作。
* **子线程**：默认情况下，子线程没有运行 `RunLoop`。如果需要使用 `RunLoop`，需要手动启动。通常来说，子线程的 `RunLoop` 主要用于处理定时器或保持线程存活。

#### 5. 使用场景

* **长时间运行的任务**：通过 `RunLoop`，可以让线程在后台处理任务或定时事件。
* **UI 更新**：在主线程中，`RunLoop` 确保 UI 可以响应用户操作和系统事件。
* **网络请求**：很多网络请求库会使用 `RunLoop` 来实现异步回调机制。

通过 `RunLoop` 的事件循环机制，系统能够在事件之间休眠，节约资源，并确保线程始终处于响应状态。在 iOS 和 macOS 项目中，`RunLoop` 是底层非常重要的机制，能够帮助管理线程生命周期、事件分发等。





***



<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p><br></p></figcaption></figure>

1. **Runloop 启动**：
   * Runloop 通常在主线程或子线程中启动，通过调用 `CFRunLoopRun` 或 `NSRunLoop run` 方法。
2. **进入主循环**：
   * Runloop 进入一个无限循环，等待并处理各种事件。
3. **处理输入源 (Input Sources)**：
   * 输入源包括文件描述符（如网络连接、文件读写）和其他输入源（如 NSPort）。
   * **处理文件描述符**：检查文件描述符是否有数据可读或可写，如果有则处理相应的事件。
   * **处理其他输入源**：处理其他类型的输入源，如 NSPort 传递的消息。
4. **处理定时器 (Timers)**：
   * 定时器用于在指定时间间隔后触发事件。
   * 检查所有注册的定时器，如果某个定时器的时间到了，则调用其回调函数。
5. **处理观察者 (Observers)**：
   * 观察者用于在特定事件发生时接收通知。
   * 检查所有注册的观察者，如果某个观察者的条件满足，则调用其回调函数。
6. **处理待处理的任务 (Pending Tasks)**：
   * 处理在 Runloop 中排队的任务，如异步任务的回调。
   * 从任务队列中取出任务并执行。
7. **空闲等待 (Wait for Next Event)**：
   * 如果当前没有需要处理的事件，Runloop 会进入空闲状态，等待下一个事件的到来。
   * 使用 `select` 或 `kqueue` 等系统调用进行阻塞等待。
8. **检查是否需要退出 (Check if Exit)**：
   * 检查是否需要退出 Runloop，通常是通过调用 `CFRunLoopStop` 或 `NSRunLoop stop` 方法。
   * **继续主循环**：如果没有退出请求，继续下一次循环。
   * **退出 Runloop**：如果有退出请求，退出 Runloop 循环。

#### 关键组件

* **输入源 (Input Sources)**：包括文件描述符和其他输入源，用于处理外部事件。
* **定时器 (Timers)**：用于在指定时间间隔后触发事件。
* **观察者 (Observers)**：用于在特定事件发生时接收通知。
* **任务队列 (Task Queue)**：用于存储待处理的任务。
* **事件循环 (Event Loop)**：主循环，不断检查并处理各种事件。

希望这个流程图和解释能帮助你更好地理解 Runloop 的内部实现逻辑。如果你有任何进一步的问题或需要更详细的解释，请随时告诉我。
