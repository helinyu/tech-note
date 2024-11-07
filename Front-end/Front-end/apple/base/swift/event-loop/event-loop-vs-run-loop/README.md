# Event Loop vs Run loop

在 Swift 中，**事件循环 (Event Loop)** 和 **Run Loop** 都是用来管理和调度事件的机制，但它们的概念和应用场景有所不同。虽然它们的功能在某些方面有相似性，但它们的使用和目的在具体实现上有所区别。让我们从这两个概念的定义、实现和作用进行对比。

#### 1. **事件循环 (Event Loop)**

事件循环是 **异步编程** 中的核心概念，广泛应用于处理并发和异步任务。事件循环的核心目的是在程序中不断检查是否有任务或事件需要处理，并分配线程来执行这些任务。事件循环通常用于 **非阻塞的异步编程**，使得应用程序在等待某些任务（例如网络请求、I/O 操作等）时不会被阻塞。

**工作原理：**

* 事件循环在一个单独的线程中运行，通常是主线程。
* 它会不断地检查任务队列，取出待处理的事件（任务）并执行。
* 当任务执行完成后，事件循环会返回并开始处理下一个任务。
* 事件循环使得多任务可以并发执行，而不会阻塞线程。

**示例：JavaScript 中的事件循环**

在 JavaScript 中，事件循环是非常常见的，处理异步事件的机制。尽管 Swift 也有类似的机制，但事件循环的概念在 JavaScript 的异步编程中更为显著。通过事件循环，JavaScript 可以在单线程的环境下处理 I/O 操作和其他异步任务，而不会阻塞主线程。

```javascript
setTimeout(() => {
    console.log("Task 1");
}, 0);

setTimeout(() => {
    console.log("Task 2");
}, 0);

console.log("Main Task");
```

输出顺序：

```
Main Task
Task 1
Task 2
```

* 即使 `setTimeout` 的延时为 `0`，`Task 1` 和 `Task 2` 仍然会在 `Main Task` 之后执行，因为事件循环首先会处理同步任务（主任务），然后才处理异步事件。

#### 2. **Run Loop (运行循环)**

`Run Loop` 是 **macOS 和 iOS** 中的一个特定的实现，用于管理事件的调度和循环处理，通常与用户界面(UI)线程相关。它用于处理系统事件（如触摸、绘制、网络、定时器等）和其他任务，并确保主线程保持响应。

**工作原理：**

* `Run Loop` 主要用于事件驱动的应用程序。它允许程序进入一个循环，等待并处理事件。
* 在 iOS 和 macOS 应用中，`Run Loop` 负责管理用户界面的事件，如触摸、按钮点击、定时器等。
* 它在主线程中运行，并会不断地检查是否有事件待处理。它能够有效地处理用户输入、后台任务、定时器等。

**运行模式：**

* **默认模式**：运行循环会监听系统事件（如触摸事件、定时器等）并执行相应的回调。
* **自定义模式**：你也可以定义自定义的事件源，并将它们添加到 `Run Loop` 中，等待处理。

**示例：Run Loop 在 iOS 中**

在 iOS 应用中，`Run Loop` 主要用于主线程（UI线程），用于处理 UI 事件和系统任务。如果没有运行循环，应用就不能响应用户输入或系统事件。

```swift
import Foundation

// 模拟阻塞任务
DispatchQueue.global().async {
    for i in 1...5 {
        print("Processing \(i)")
        sleep(1)
    }
}

// Run Loop 保持活跃并处理事件
RunLoop.main.run()  // 使应用保持运行
```

* 上面代码中的 `RunLoop.main.run()` 确保主线程不会退出，允许应用继续运行并响应用户交互。否则，主线程会在执行完其他任务后退出，应用就无法响应用户输入了。

#### 3. **对比总结**

| 特性         | 事件循环 (Event Loop)                     | Run Loop                           |
| ---------- | ------------------------------------- | ---------------------------------- |
| **目的**     | 处理并发任务、异步事件，保证任务不阻塞线程                 | 处理 UI 事件、系统事件，并保持主线程活跃             |
| **使用场景**   | 异步编程框架、并发任务调度、非阻塞 I/O 操作              | 用户界面线程、处理系统事件和用户输入                 |
| **处理方式**   | 检查并执行队列中的任务，适用于异步任务和回调的执行             | 主要在主线程中运行，用于处理 UI 事件、定时器和后台任务等     |
| **线程**     | 通常运行在单线程上，常用于事件驱动模型                   | 通常运行在主线程中，处理 UI 更新、用户输入等事件         |
| **异步任务处理** | 通过事件循环机制让异步任务并发执行而不阻塞主线程              | 通过运行循环机制处理 UI 事件和其他事件，保证应用响应性      |
| **常见框架**   | 用于非阻塞编程（例如 JavaScript、Swift 中的异步任务调度） | iOS 和 macOS 中的事件驱动机制，应用程序 UI 响应的核心 |

#### 4. **如何理解它们的区别**

* **事件循环** 是一种 **通用机制**，用于管理和调度任务，通常用于异步编程中，事件循环会调度多个异步任务（例如网络请求或定时任务），并将它们放入队列中逐个执行。在一些编程环境（如 Node.js、JavaScript）中，事件循环非常显著。
* **Run Loop** 是 macOS 和 iOS 中的 **特定实现**，它主要用于管理主线程中的 UI 事件和后台任务，确保应用的响应性。在 iOS/macOS 中，应用程序的生命周期通常依赖于 `Run Loop` 来处理事件和保持线程的活跃状态。

#### 5. **事件循环与 Run Loop 在 Swift 中的关系**

在 Swift 中，`async/await` 和 `Combine` 这类异步编程模型本质上与 **事件循环** 紧密相关。Swift 的异步任务系统（例如，`Task`）通常依赖于 **事件循环** 来管理任务的调度。而 `Run Loop` 则通常与 UI 线程有关，主要用于处理系统级事件并确保应用响应。

虽然 **事件循环** 和 **Run Loop** 都是任务调度和事件处理的机制，但 **事件循环** 更关注 **异步编程** 和 **任务调度**，而 **Run Loop** 更关注 **UI 线程** 的事件处理和系统任务。

#### 总结

* **事件循环 (Event Loop)** 是一种用来处理异步任务、事件流和并发操作的机制，通常用于非阻塞的异步编程。
* **Run Loop** 主要是 iOS 和 macOS 中处理 UI 和系统事件的机制，通常用于保持主线程活跃，响应用户输入和系统事件。

它们虽然看似有相似的功能，都是用来处理事件，但各自的作用和应用场景有很大不同。