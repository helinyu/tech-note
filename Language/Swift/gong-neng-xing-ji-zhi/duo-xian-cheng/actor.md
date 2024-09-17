# Actor

在Swift中，`Actor` 是一种并发编程模型，用于处理并发任务和共享状态。它于Swift 5.5中引入，并在后续版本中得到了进一步的完善。

`actor` 是用于封装状态和执行并发操作的类型，它**确保了在同一时间只有一个线程（或任务）可以访问其内部状态，从而避免了数据竞争和其他并发问题。**



## 1、actor 的基本特性

1. **封装性**：`actor` 封装了它的状态和执行这些状态操作的代码。这意味着，所有对`actor`内部状态的访问都必须通过`actor`自身的方法来进行。
2. **隔离性**：`actor` 的方法默认是隔离的（isolated），这意味着在任何给定时间，只有一个线程（或任务）可以执行`actor`的某个方法。这种隔离性保证了并发安全。
3. **非阻塞**：虽然`actor`的方法默认是串行执行的，但Swift的并发模型允许你使用`async`/`await`来编写非阻塞的并发代码。这意味着，当你等待一个`actor`方法完成时，你可以同时执行其他任务。
4. **消息传递**：当你从一个线程（或任务）向`actor`发送消息（即调用其方法）时，该消息会被排队并在`actor`的上下文中串行处理。这类似于传统并发模型中的消息传递机制。

#### 如何定义和使用 actor

在Swift中，你可以使用`actor`关键字来定义一个`actor`类型。例如：

```swift
actor Counter {  
    private var count = 0  
  
    func increment() async {  
        count += 1  
    }  
  
    func getCount() -> Int {  
        return count  
    }  
}
```

注意，在这个例子中，`increment` 方法被标记为`async`，因为它修改了`actor`的内部状态，并且可能需要等待（尽管在这个简单的例子中它并没有）。而`getCount` 方法没有标记为`async`，因为它只是读取`actor`的状态而不进行修改。然而，由于`actor`的隔离性，直接从`actor`外部调用`getCount` 可能不会总是返回最新的值，因为当你读取`count`时，另一个任务可能已经修改了它。为了避免这个问题，你可以将`getCount` 也标记为`async` 并返回一个未来的值（如`async` 函数通常所做的那样），但在这个简单的例子中，我们假设你了解这一点并在使用时进行了适当的同步。

#### 注意事项

* `actor` 的方法<mark style="color:red;">默认是隔离的</mark>，这意味着你不能直接从`actor`外部访问其属性。如果你需要这样做，你应该通过`actor`的方法来进行。
* 当你从`actor`外部调用一个<mark style="color:red;">`async`</mark> <mark style="color:red;"></mark><mark style="color:red;">方法时，你应该使用</mark><mark style="color:red;">`await`</mark> 关键字来等待结果，除非你有其他方式来处理异步性（如使用`Task`）。
* `actor` 之间的<mark style="color:orange;">通信通常是通过调用对方的方法来进行的</mark>，这有助于保持代码的清晰和可维护性。
* `actor` 的使用应该谨慎，因为它们**可能会引入额外的开销和复杂性**。在不需要并发安全性的地方，你应该考虑使用其他类型的并发模型或数据结构。



## 2、使用

#### 1. 定义 Actor

首先，你需要定义一个 `Actor` 类型。`Actor` 类型必须遵循 `Actor` 协议，并且它的属性和方法必须是 `nonmutating` 的。

```swift
import Foundation

actor MyActor {
    var counter = 0
    
    func increment() {
        counter += 1
    }
    
    func getCounter() -> Int {
        return counter
    }
}
```

#### 2. 创建 Actor 实例

你可以像创建普通类实例一样创建 `Actor` 实例。

```swift
let myActor = MyActor()
```

#### 3. 在 Actor 上调用方法

要调用 `Actor` 上的方法，你需要使用 `async` 关键字，并且必须在 `async` 函数或 `Task` 中进行。

```swift
Task {
    await myActor.increment()
    let count = await myActor.getCounter()
    print("Counter: \(count)")
}
```

#### 4. 使用 `async let` 并发执行

你可以使用 `async let` 来并发执行多个 `Actor` 方法调用。

```swift
Task {
    async let count1 = myActor.getCounter()
    async let count2 = myActor.increment()
    
    let results = await (count1, count2)
    print("Results: \(results)")
}
```

#### 5. 使用 `await` 等待结果

在调用 `Actor` 方法时，你需要使用 `await` 关键字来等待结果。

```swift
Task {
    let count = await myActor.getCounter()
    print("Counter: \(count)")
}
```

#### 6. 使用 `withCheckedContinuation` 进行回调

如果你需要在 `Actor` 方法完成后执行某些操作，可以使用 `withCheckedContinuation`。

```swift
Task {
    myActor.getCounter().withCheckedContinuation { continuation in
        continuation.resume(returning: 42)
    }
}
```

#### 7. 使用 `async` 和 `await` 进行异步编程

`Actor` 模型与 Swift 的 `async` 和 `await` 异步编程模型紧密结合，使得编写并发代码更加简单和安全。

```swift
Task {
    await myActor.increment()
    let count = await myActor.getCounter()
    print("Counter: \(count)")
}
```

通过这些步骤和示例，你可以看到如何在 Swift 中使用 `Actor` 来处理并发任务和共享状态。`Actor` 模型提供了一种安全且高效的方式来管理并发，避免了数据竞争和并发问题。
