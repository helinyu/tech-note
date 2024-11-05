# 发布者

在 Combine 框架中，发布者（Publishers）是指发出数据流并将其传递给订阅者的组件。Combine 提供了多种类型的发布者，每种类型都可以发出不同种类的数据或事件。以下是一些常见的发布者类型：

1. [<mark style="color:red;">**Just**</mark><mark style="color:red;">:</mark>](just/)
   * 用于发布单一的值，并在发布后完成。
   *   示例：

       ```swift
       let publisher = Just("Hello, Combine!")
       ```
2. **Publishers.Sequence**:
   * 用于发布序列中的元素，通常用于数组、集合等数据结构。
   *   示例：

       ```swift
       let publisher = Publishers.Sequence(sequence: [1, 2, 3, 4, 5])
       ```
3. **Publishers.Timer**:
   * 用于在定时间隔内发布时间。
   *   示例：

       ```swift
       let publisher = Publishers.Timer(every: .seconds(1), tolerance: .milliseconds(100), scheduler: RunLoop.main, options: nil)
       ```
4. <mark style="color:red;">**PassthroughSubject**</mark>:
   * 一个允许手动发送值的发布者，它不像 `Just` 或 `Sequence` 那样固定数据流，可以动态发送数据。
   *   示例：

       ```swift
       let subject = PassthroughSubject<String, Never>()
       subject.send("New message")
       ```
5. <mark style="color:red;">**CurrentValueSubject**</mark><mark style="color:red;">:</mark>
   * 类似于 `PassthroughSubject`，但它始终保持并发布一个当前值。它允许订阅者获取当前值并监听后续更新。
   *   示例：

       ```swift
       let subject = CurrentValueSubject<Int, Never>(0)
       subject.send(1)
       ```
6. [<mark style="color:red;">**Future**</mark><mark style="color:red;">:</mark>](future.md)
   * 用于包装一个异步任务，最终发布一个值或错误。
   *   示例：

       ```swift
       let publisher = Future<String, Error> { promise in
           // 进行异步操作
           promise(.success("Async Result"))
       }
       ```
7. **NotificationCenter.Publisher**:
   * 用于通过通知中心发布通知。
   *   示例：

       ```swift
       let publisher = NotificationCenter.default.publisher(for: .NSWorkspaceDidWakeNotification)
       ```
8. **URLSession.DataTaskPublisher**:
   * 用于发布网络请求的响应数据。
   *   示例：

       ```swift
       let publisher = URLSession.shared.dataTaskPublisher(for: URL(string: "https://example.com")!)
       ```
9. **CombineLatest**:
   * 用于将多个发布者的最新值合并成一个元组发布。
   *   示例：

       ```swift
       let publisher1 = Just(1)
       let publisher2 = Just(2)
       let combined = Publishers.CombineLatest(publisher1, publisher2)
       ```
10. **Merge**:
    * 用于将多个发布者的数据流合并为一个。
    *   示例：

        ```swift
        let publisher1 = Just(1)
        let publisher2 = Just(2)
        let merged = Publishers.Merge(publisher1, publisher2)
        ```
11. [**Deferred**](deferred.md)：

* 延迟创建发布者直到有订阅者时。它可以根据提供的闭包创建一个新的发布者实例。
* 例如：`Deferred { Just(10) }` 在订阅时才会创建并发布值 10。

12. **Array.publisher**：

* 用于将数组转换为 Combine 发布者，将数组的每个元素依次发布。
* 例如：`[1, 2, 3].publisher` 会依次发布 1, 2, 3。
