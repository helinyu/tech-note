# 基本概念

它用于<mark style="color:red;">处理异步事件和数据流</mark>，并通过<mark style="color:red;">声明式</mark>的方式使得代码更清晰易懂。&#x20;

处理异步事件

数据流： 就是响应式编程实现的



以下是 Combine 框架的一些基本概念：

1. **Publisher（发布者）**：
   * 发布者是一个可以发布值的对象，它会在值可用时发出通知。
   * 例如，`Just`、`Future`、`NotificationCenter.Publisher` 等都是 Combine 提供的发布者类型。
2. **Subscriber（订阅者）**：
   * 订阅者是一个接收和处理来自发布者的值的对象。
   * 订阅者可以通过实现 `Subscriber` 协议来定义其处理逻辑。
3. **Subject（主题）**：
   * 主题是一种特殊的发布者，它允许手动发送值。
   * Combine 提供了多种类型的主题，如 `PassthroughSubject` 和 `CurrentValueSubject`，前者用于发送值而不保持任何状态，后者用于保持最后一个值的状态。
4. **Operators（操作符）**：
   * Combine 提供了一组丰富的操作符，用于处理、变换和组合发布者发出的值。
   * 常见的操作符包括 `map`、`filter`、`combineLatest`、`merge` 等。
5. **Cancellables（可取消的）**：
   * 订阅一个发布者会返回一个 `Cancellable` 对象，通过调用它的 `cancel()` 方法，可以停止接收值。
   * 这在需要释放资源或停止更新时非常有用。
6. **Schedulers（调度器）**：
   * 调度器用于控制代码在何时以及在哪个线程上执行。
   * Combine 提供了一些内置的调度器，如 `DispatchQueue.main` 和 `RunLoop.main`，用于在主线程上执行 UI 更新。
7. **Backpressure（背压）**：
   * 背压是指在生产者（发布者）生成数据的速度超过消费者（订阅者）处理速度时，如何控制数据流动。
   * Combine 通过使用 `Demand` 来管理背压。

Combine 框架使得处理异步数据流变得更加简单和直观，通过这些基本概念，你可以构建响应式应用程序，并有效管理数据流和事件。
