# 同时是发送者和接受者

在 Combine 框架中，`Publisher` 是发送者，`Subscriber` 是接受者。在某些场景下，一个对象既充当发送者（Publisher），又充当接受者（Subscriber），这种情况通常发生在一些需要双向数据流或需要处理自定义逻辑的地方。

如果你是指某个对象既发布事件又订阅事件，可以考虑以下方式：

1. **双向绑定**：对象既可以作为 `Publisher`（发送者）发布数据，也可以作为 `Subscriber`（接受者）订阅其他的 `Publisher`。
2. **Subject**：`Subject` 既是 `Publisher` 又是 `Subscriber`，它允许你手动发送事件，也能接收来自其他 `Publisher` 的事件。

#### 示例：使用 `PassthroughSubject`

```swift
import Combine

class MyPublisherSubscriber {
    var cancellables = Set<AnyCancellable>()
    var subject = PassthroughSubject<String, Never>()

    init() {
        // 作为 Subscriber 订阅自己发布的事件
        subject
            .sink { value in
                print("Received: \(value)")
            }
            .store(in: &cancellables)
        
        // 作为 Publisher 发布事件
        subject.send("Hello, Combine!")
    }
}

let example = MyPublisherSubscriber()
```

在这个例子中，`subject` 作为 `PassthroughSubject` 实现了同时作为发布者和订阅者的角色。它首先订阅自己发布的事件，接着发送了一个字符串事件 `"Hello, Combine!"`。
