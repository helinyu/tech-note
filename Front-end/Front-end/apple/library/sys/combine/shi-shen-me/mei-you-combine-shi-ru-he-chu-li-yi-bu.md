# 没有Combine是如何处理异步

在没有 Combine 的情况下，Swift 中的异步编程通常依赖于传统的异步处理方式，包括 **回调函数（Completion Handlers）**、**GCD（Grand Central Dispatch）**、**OperationQueue** 和 **代理（Delegate）** 等方法。这些方法能够处理异步任务，但每种方式的使用场景和设计模式不同。

#### 1. **回调函数（Completion Handlers）**

回调函数是处理异步操作的经典方式。异步任务执行完后，调用提供的回调函数来通知结果。这种方法广泛用于网络请求、文件操作等异步任务中。

**示例代码：**

```swift
func fetchData(completion: @escaping (Result<Data, Error>) -> Void) {
    // 异步任务：模拟网络请求
    DispatchQueue.global().async {
        // 假设任务完成
        let data = Data() // 模拟的数据
        completion(.success(data)) // 调用回调函数
    }
}

// 使用回调
fetchData { result in
    switch result {
    case .success(let data):
        print("获取到数据：\(data)")
    case .failure(let error):
        print("发生错误：\(error)")
    }
}
```

**缺点**：回调地狱（Callback Hell），当多个异步操作嵌套时，代码变得难以阅读和维护。

#### 2. **GCD（Grand Central Dispatch）**

GCD 是处理多线程和并发操作的低级别 API，广泛用于执行并行任务和更新 UI。通过 `DispatchQueue`，你可以将任务分配到不同的队列（主队列或后台队列）中执行。

**示例代码：**

```swift
// 异步任务执行在全局队列中
DispatchQueue.global().async {
    let result = heavyComputation() // 长时间计算任务
    DispatchQueue.main.async {
        // 在主队列更新 UI
        updateUI(with: result)
    }
}
```

**优点**：简单且灵活，适用于大多数并发任务和线程管理。 **缺点**：需要手动管理线程和任务的调度，难以处理复杂的异步逻辑和数据流。

#### 3. **OperationQueue**

`OperationQueue` 是对 GCD 的高级封装，提供了更多的功能，如任务依赖、优先级控制和取消操作等。它适合用于更复杂的任务管理。

**示例代码：**

```swift
let queue = OperationQueue()

let operation = BlockOperation {
    let result = heavyComputation()
    DispatchQueue.main.async {
        updateUI(with: result)
    }
}

queue.addOperation(operation)
```

**优点**：可以管理任务的依赖关系和优先级，并且支持取消任务。 **缺点**：比 GCD 更加复杂，适合处理多个任务之间有依赖关系的场景。

#### 4. **代理（Delegate）模式**

代理模式用于将事件或操作从一个对象传递到另一个对象。在异步编程中，代理通常用于通知任务的完成、更新或错误。

**示例代码：**

```swift
protocol DataFetcherDelegate: AnyObject {
    func didFetchData(_ data: Data)
    func didFailWithError(_ error: Error)
}

class DataFetcher {
    weak var delegate: DataFetcherDelegate?
    
    func fetchData() {
        // 异步任务模拟
        DispatchQueue.global().async {
            let data = Data() // 模拟数据
            DispatchQueue.main.async {
                self.delegate?.didFetchData(data) // 通知代理
            }
        }
    }
}

// 使用代理
class ViewController: UIViewController, DataFetcherDelegate {
    func didFetchData(_ data: Data) {
        print("数据获取完成：\(data)")
    }
    
    func didFailWithError(_ error: Error) {
        print("发生错误：\(error)")
    }
    
    func fetchData() {
        let fetcher = DataFetcher()
        fetcher.delegate = self
        fetcher.fetchData()
    }
}
```

**优点**：适合用于组件间通信，尤其是在 UIKit 中，很多组件如 `UITableView` 或 `UICollectionView` 都是通过代理模式与其他对象进行交互的。 **缺点**：对于多个异步任务的处理可能会导致代理的逻辑变得复杂，维护难度较大。

#### 5. **NotificationCenter（通知中心）**

`NotificationCenter` 是一个发布-订阅模式的实现，可以让对象在应用程序中广播消息并让其他对象监听这些消息。这是另一种在异步操作中传递结果的方式。

**示例代码：**

```swift
// 发送通知
NotificationCenter.default.post(name: .dataFetched, object: nil, userInfo: ["data": someData])

// 监听通知
NotificationCenter.default.addObserver(self, selector: #selector(handleData(_:)), name: .dataFetched, object: nil)

@objc func handleData(_ notification: Notification) {
    if let data = notification.userInfo?["data"] as? Data {
        print("收到数据：\(data)")
    }
}
```

**优点**：可以广播消息给多个监听者，适合全局事件通知。 **缺点**：无法传递数据流，且容易导致内存泄漏，尤其是没有正确移除观察者时。

#### 6. **`async` 和 `await`（Swift 5.5 引入）**

从 Swift 5.5 开始，Swift 引入了 `async` 和 `await` 关键字，用于处理异步操作。它们提供了一种简洁、直观的方式来处理异步编程，类似于其他语言（如 JavaScript 或 Kotlin）中的协程。

**示例代码：**

```swift
func fetchData() async throws -> Data {
    // 异步操作
    return try await someAsyncNetworkCall()
}

// 调用异步函数
Task {
    do {
        let data = try await fetchData()
        print("获取到数据：\(data)")
    } catch {
        print("错误：\(error)")
    }
}
```

**优点**：语法简洁，使用 `async` 和 `await` 可以更清晰地表达异步操作，避免回调地狱问题。 **缺点**：只能在支持的环境（如 Swift 5.5 及以上）中使用，且对于复杂的异步任务可能需要结合其他机制（如 `TaskGroup`）来处理并发。

#### 总结

在没有 Combine 的情况下，异步编程依赖于以下方式：

* **回调函数**（Completion Handlers）：传统的方式，适合处理单一异步任务，但容易导致回调地狱。
* **GCD 和 OperationQueue**：处理多线程任务，适合并发操作，但需要手动管理。
* **代理和 NotificationCenter**：用于对象间的事件传递，但不直接处理数据流。
* **`async` / `await`**：Swift 5.5 引入的现代异步编程方法，提供了更简洁的语法，解决了回调地狱问题。

这些方法虽然能够有效处理异步操作，但通常需要更多的手动管理和代码结构设计，而 Combine 提供了更高级的抽象，可以更方便地处理异步操作、数据流和响应式编程。
