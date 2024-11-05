# async/await

在 Swift 中，`async` 和 `await` 是用于异步编程的重要关键字，引入于 Swift 5.5。它们使得异步代码的编写更加简洁和易于理解，并且可以避免使用复杂的回调或闭包，从而简化了异步操作的逻辑。

#### 1. **`async` 关键字**

`async` 用于定义**异步函数**，意味着该函数的执行将不会阻塞当前线程，它将异步执行并返回一个异步结果。要调用这个异步函数时，必须使用 `await` 来等待其完成。

**示例：**

```swift
func fetchData() async -> String {
    // 模拟异步操作（比如网络请求或读取文件）
    return "Fetched Data"
}
```

* 上述代码中，`fetchData` 函数是一个异步函数，返回一个 `String` 类型的结果。要调用这个函数，你不能直接调用它，而是需要使用 `await`。

#### 2. **`await` 关键字**

`await` 用来等待一个异步函数执行的结果。它只能在异步函数内使用，它会暂停当前的执行，直到异步操作完成。

**示例：**

```swift
func processData() async {
    let data = await fetchData()  // 使用 await 等待 fetchData 完成
    print("Processed: \(data)")
}
```

* 在上面的代码中，`await fetchData()` 表示我们等待 `fetchData()` 函数完成，并返回结果后再继续执行 `processData()` 中的后续代码。

#### 3. **如何启动异步任务**

与传统的同步函数调用不同，异步函数通常是在一个异步上下文（如异步函数或任务）中执行。为了启动异步操作，Swift 使用了 `Task` 来创建一个异步任务。

**示例：**

```swift
Task {
    await processData()  // 在异步任务中调用异步函数
}
```

* `Task` 是用于启动异步操作的容器，它会在后台线程中执行异步函数，并且 `await` 会确保代码执行顺序。

#### 4. **`async` / `await` 在并发中的应用**

异步编程特别适用于**并发操作**，例如多个网络请求或文件读取等任务。通过 `async` 和 `await`，你可以轻松地并行执行多个异步任务，并等待它们完成。

**示例：**

```swift
func fetchDataFromAPI1() async -> String {
    return "Data from API 1"
}

func fetchDataFromAPI2() async -> String {
    return "Data from API 2"
}

func fetchData() async {
    async let api1 = fetchDataFromAPI1()  // 异步启动请求
    async let api2 = fetchDataFromAPI2()  // 异步启动请求
    
    let data1 = await api1  // 等待 fetchDataFromAPI1 完成
    let data2 = await api2  // 等待 fetchDataFromAPI2 完成
    
    print("Fetched \(data1) and \(data2)")
}
```

* 在上面的代码中，`async let` 用来启动多个异步操作，它们会并行执行。当你使用 `await` 获取结果时，程序会等待所有异步任务完成。

#### 5. **错误处理**

与同步函数一样，异步函数也可以抛出错误（`throw`），你可以在异步函数中使用 `try`、`catch` 来捕获和处理错误。

**示例：**

```swift
enum DataError: Error {
    case noData
}

func fetchDataWithError() async throws -> String {
    throw DataError.noData
}

func processData() async {
    do {
        let data = try await fetchDataWithError()
        print("Data: \(data)")
    } catch {
        print("Error: \(error)")
    }
}
```

* 这里，`fetchDataWithError` 函数是一个抛出错误的异步函数，在 `processData` 中，我们使用 `try await` 来等待并处理可能发生的错误。

#### 6. **`async` / `await` 和 UI 更新**

在 iOS 或 macOS 应用中，通常需要在主线程中更新 UI。尽管 `async` 和 `await` 允许异步执行操作，但它们仍然会将结果返回到主线程，以确保 UI 更新的线程安全。

**示例：**

```swift
func fetchData() async -> String {
    // 模拟网络请求
    return "Fetched Data"
}

func updateUI() async {
    let data = await fetchData()
    DispatchQueue.main.async {
        // 更新UI代码
        print("UI updated with: \(data)")
    }
}
```

* 在上述代码中，我们使用 `await` 获取数据后，通过 `DispatchQueue.main.async` 将 UI 更新代码切换回主线程。

#### 7. **使用 `async/await` 的好处**

* **简洁和易读**：`async` 和 `await` 可以使异步代码看起来像同步代码，减少回调函数的嵌套（“回调地狱”）。
* **并发执行**：可以并行执行多个异步操作（如并发的网络请求），提高应用的性能。
* **错误处理**：可以使用 `try`、`catch` 来处理异步函数中的错误，避免了传统回调中的错误处理复杂性。
* **UI流畅**：可以避免阻塞主线程，保持应用界面的响应。

#### 总结

在 Swift 中，`async` 和 `await` 是实现异步编程的重要工具。通过这两个关键字，开发者能够简洁地编写并发任务，使得异步操作更加直观、易于管理。无论是进行并发的网络请求，还是处理复杂的异步任务，`async` 和 `await` 都提供了一种更加现代化的编程方式。
