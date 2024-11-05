# 类型

在 Combine 框架中，作为既是发送者（Publisher）也是接受者（Subscriber）的类型，主要是通过 **Subject** 实现的。`Subject` 是 Combine 中一个特殊的类型，它既能作为 `Publisher` 发布事件，也能作为 `Subscriber` 接收事件。常用的 `Subject` 类型有：

#### 1. **PassthroughSubject**

`PassthroughSubject` 是一种简单的 `Subject`，它作为 `Publisher` 发出事件，作为 `Subscriber` 接收事件。它是最常见的实现方式之一，通常用于手动发送事件。

```swift
let passthroughSubject = PassthroughSubject<String, Never>()

// 作为 Publisher 发送事件
passthroughSubject.send("Hello")

// 作为 Subscriber 订阅事件
passthroughSubject
    .sink { value in
        print("Received: \(value)")
    }
    .store(in: &cancellables)
```

#### 2. **CurrentValueSubject**

`CurrentValueSubject` 是<mark style="color:orange;">一个有初始值的</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`Subject`</mark>。它不仅可以作为 `Publisher` 发布当前值和新的事件，还能保持和访问当前的最新值。它的初始化需要一个初始值，因此在开始使用时会有一个 "初始状态"。

```swift
let currentValueSubject = CurrentValueSubject<String, Never>("Initial Value")

// 作为 Publisher 发送事件
currentValueSubject.send("Updated Value")

// 作为 Subscriber 订阅事件
currentValueSubject
    .sink { value in
        print("Received: \(value)")
    }
    .store(in: &cancellables)

// 可以访问当前值
print(currentValueSubject.value)  // "Updated Value"
```

#### 3. **ReplaySubject** (通过自定义实现)

Combine 原生没有 `ReplaySubject`，但是可以通过自定义 `Publisher` 来实现一个类似的功能。`ReplaySubject` 通常会缓存一段时间内发布的值，并且能够将这些值重新发送给新的订阅者。

你可以通过自定义 `Publisher` 和缓存机制来模拟这个功能：

```swift
// 简单的自定义缓存机制来模拟 ReplaySubject
class ReplaySubject<Value, Failure: Error>: Publisher {
    private var cache: [Value] = []
    private let subject = PassthroughSubject<Value, Failure>()
    
    func send(_ value: Value) {
        cache.append(value)
        subject.send(value)
    }
    
    func receive<S>(subscriber: S) where S : Subscriber, Failure == S.Failure, Value == S.Input {
        // 发送缓存的所有值
        cache.forEach { subscriber.receive($0) }
        subject.receive(subscriber: subscriber)
    }
}
```

#### 4. **AnyPublisher**

`AnyPublisher` 是一种将任何符合 `Publisher` 协议的类型封装成统一类型的工具。它本身并不是 `Subject`，但可以通过它将不同的 `Publisher` 组合或转换成统一的类型。因此，`AnyPublisher` 本身不直接充当发送者或接受者，但可以用来将不同的 `Publisher` 进行抽象，间接地实现类似的功能。

```swift
let anyPublisher: AnyPublisher<String, Never> = passthroughSubject.eraseToAnyPublisher()
```

#### 总结：

在 Combine 中，主要通过 **Subject** 来实现既作为发送者又作为接收者的功能。常用的 `Subject` 类型包括：

* **PassthroughSubject**：最常用的 `Subject`，适合简单的事件传递。
* **CurrentValueSubject**：有初始值的 `Subject`，适合需要持有和访问最新值的场景。
* **ReplaySubject**：Combine 中没有内建，但可以通过自定义来实现，适用于缓存事件并重新发送给新的订阅者。

你可以根据需要选择不同类型的 `Subject` 来实现你想要的功能。如果有具体需求，欢迎分享，我可以帮助提供更多的实现细节！
