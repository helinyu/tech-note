# async/wait(协程) vs Combine(线程)

`async/await` 和 `Combine` 在底层实现上有所不同，但它们的区别主要是编程模型和抽象方式，而不是简单地基于“协程”或“线程”。

* **async/await**：确实是基于 Swift 协程（coroutines）实现的，它允许你编写异步代码时看起来像是同步代码。这种异步特性并不依赖于线程，而是利用 Swift 运行时来挂起和恢复任务。`async/await` 会在必要时自动切换执行上下文，但这个切换未必总是涉及到线程的切换。
* **Combine**：是苹果的响应式编程框架，用于处理异步数据流。它基于 Publisher 和 Subscriber 模型来传递数据，主要通过调度器（DispatchQueue 或 OperationQueue）管理线程和调度工作。因此，Combine 可以通过调度器控制代码在不同线程上执行，但它本身并不直接使用协程来实现异步任务。

简单来说，

`async/await` 是<mark style="color:red;">协程的实现方式</mark>，

&#x20;`Combine` <mark style="color:red;">依赖线程调度和调度器来处理异步数据流</mark>。

两者的实现机制不同，但并不意味着 `Combine` 就是基于线程的。
