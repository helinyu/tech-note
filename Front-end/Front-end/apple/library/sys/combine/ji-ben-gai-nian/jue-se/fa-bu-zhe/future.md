# Future

在 Swift 中，`Combine` 框架提供了 `Future` 类型，用于<mark style="color:red;">表示一个异步操作的结果</mark>，<mark style="color:orange;">它最终会返回一个值或错误。</mark><mark style="color:blue;">`Future`</mark> <mark style="color:blue;"></mark><mark style="color:blue;">是一个封装了延迟计算结果的</mark> <mark style="color:blue;"></mark><mark style="color:blue;">`Publisher`</mark><mark style="color:blue;">，通常用来处理那些会在未来某个时刻完成的操作</mark>，例如网络请求、数据库查询或其他异步任务。

`Future` 类型符合 `Publisher` 协议，这意味着它可以被订阅，并且会发出一个值或者错误。其基本用法如下：

#### 1. 创建一个 `Future` 实例

`Future` 的初始化需要一个闭包，该闭包接受一个 `@escaping` 的 `Promise` 参数，`Promise` 用于将结果传递给订阅者：

```swift
import Combine

let future = Future<Int, Error> { promise in
    // 假设我们有一个异步操作
    DispatchQueue.global().asyncAfter(deadline: .now() + 2) {
        // 操作完成，返回结果
        promise(.success(42))  // 你可以选择调用 .failure(error) 来返回错误
    }
}
```

#### 2. 订阅 `Future`

一旦 `Future` 被创建并且开始执行，你可以通过 `sink` 或 `receive(subscriber:)` 来订阅它：

```swift
future.sink { completion in
    switch completion {
    case .finished:
        print("Future completed successfully")
    case .failure(let error):
        print("Future failed with error: \(error)")
    }
} receiveValue: { value in
    print("Received value: \(value)")
}
```

#### 3. 处理多次结果

由于 `Future` 只会发出一个值（成功或失败），它是一个一次性的流。如果你需要处理多个值的流，应考虑使用其他类型的 Publisher，例如 `Just` 或 `PassthroughSubject`。

#### 4. 错误处理

`Future` 可以通过 `promise(.failure(error))` 来发出错误，在订阅者中可以通过 `completion` 捕获：

```swift
let errorFuture = Future<String, Error> { promise in
    DispatchQueue.global().asyncAfter(deadline: .now() + 1) {
        promise(.failure(NSError(domain: "com.example.error", code: 1, userInfo: nil)))
    }
}

errorFuture.sink { completion in
    switch completion {
    case .finished:
        print("No error.")
    case .failure(let error):
        print("Error occurred: \(error)")
    }
} receiveValue: { value in
    print(value)
}
```

#### 5. 结合其他 Publisher 使用

`Future` 可以与其他 `Publisher` 类型配合使用，例如链式调用、`map`、`flatMap` 等操作符。例如，结合 `map` 转换返回值：

```swift
future
    .map { value in
        return "The result is \(value)"
    }
    .sink { completion in
        switch completion {
        case .finished:
            print("Finished successfully")
        case .failure(let error):
            print("Failed with error: \(error)")
        }
    } receiveValue: { transformedValue in
        print(transformedValue)
    }
```

#### 总结

`Future` 是 `Combine` 中一个很有用的类型，它帮助你处理那些异步执行、且只会返回一个结果的操作。它与其他 `Publisher` 类型一样，可以通过操作符进行链式调用和错误处理。
