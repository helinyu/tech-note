# Task

在 Swift 中，`Task` 是一种用于表示异步计算的结构体。它是 Swift 并发编程模型的核心组成部分，允许你以声明式的方式编写异步代码。`Task` 可以让你轻松地启动、管理和监控异步操作。

#### 创建 Task

你可以使用 `Task` 构造函数来创建一个新的 `Task`。通常，你会在一个 `async` 函数内部创建 `Task`，以便它可以异步执行。

```swift
func startAsyncTask() async {
    let task = Task {
        // 异步操作
        await someAsyncFunction()
    }
}
```

#### 启动 Task

创建 `Task` 后，它会自动启动并开始执行异步操作。你不需要显式调用任何方法来启动它。

```swift
func startAsyncTask() async {
    let task = Task {
        // 异步操作
        await someAsyncFunction()
    }
}
```

#### 等待 Task 完成

你可以使用 `await` 关键字来等待 `Task` 完成。这会暂停当前 `async` 函数的执行，直到 `Task` 完成为止。

```swift
func startAsyncTask() async {
    let task = Task {
        // 异步操作
        await someAsyncFunction()
    }
    
    await task.value // 等待任务完成并获取结果
}
```

#### 取消 Task

你可以使用 `cancel()` 方法来取消一个 `Task`。取消操作会立即停止 `Task` 的执行，并抛出一个 `CancellationError` 异常。

```swift
func startAsyncTask() async {
    let task = Task {
        try await withUnsafeThrowingContinuation { continuation in
            // 异步操作
            continuation.resume(throwing: CancellationError())
        }
    }
    
    task.cancel() // 取消任务
}
```

#### 监控 Task 状态

你可以使用 `Task.Status` 枚举来监控 `Task` 的状态。`Task.Status` 有以下几种可能的值：

* `.active`: `Task` 正在执行。
* `.suspended`: `Task` 已暂停。
* `.cancelled`: `Tas`k 已取消。
* `.finished`: `Task` 已完成。

```swift
func monitorTaskStatus() async {
    let task = Task {
        // 异步操作
        await someAsyncFunction()
    }
    
    while !task.isCancelled {
        switch task.status {
        case .active:
            print("Task is active")
        case .suspended:
            print("Task is suspended")
        case .cancelled:
            print("Task is cancelled")
        case .finished:
            print("Task is finished")
        @unknown default:
            break
        }
        
        try? await Task.sleep(nanoseconds: 1_000_000_000) // 每秒检查一次状态
    }
}
```

#### 使用 `async let` 并发执行多个 Task

你可以使用 `async let` 来并发执行多个 `Task`，并在所有 `Task` 完成后处理它们的结果。

```swift
func concurrentTasks() async {
    async let task1 = someAsyncFunction1()
    async let task2 = someAsyncFunction2()
    
    let (result1, result2) = await (task1, task2)
    print("Results: \(result1), \(result->2)")
}
```

通过这些示例，你可以看到如何在 Swift 中使用 `Task` 来编写异步代码。`Task` 提供了一种简单且强大的方式来管理异步操作，使得编写并发代码更加容易和安全。
