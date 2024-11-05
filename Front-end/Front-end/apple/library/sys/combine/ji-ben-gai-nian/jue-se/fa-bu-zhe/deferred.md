# Deferred

在 `Combine` 框架中，`Deferred` 是一个用于创建 `Publisher` 的结构，允许你在每次订阅时动态地生成一个新的 `Publisher`。这种方式非常适合于需要在每次订阅时都要执行某种逻辑的场景，比如延迟执行、条件创建或动态配置的情况。

#### `Deferred` 的特点

1. **延迟创建**：`Deferred` 不会在创建时立即生成 `Publisher`，而是在每次订阅时生成新的 `Publisher`。这使得它适用于需要动态决定如何处理数据的场景。
2. **懒加载**：它可以用于懒加载 `Publisher` 的逻辑，只有在实际需要时才会执行创建逻辑。
3. **可重用性**：每次新的订阅都会生成一个新的 `Publisher`，因此可以保持订阅的独立性，彼此之间互不干扰。

#### 基本用法

`Deferred` 的基本用法是使用一个闭包来创建 `Publisher`，这个闭包将在每次订阅时执行。下面是一个简单的示例，展示如何使用 `Deferred` 创建一个 `Publisher`。

```swift
import Combine

let deferredPublisher = Deferred {
    Just(Int.random(in: 1...100)) // 在每次订阅时生成一个新的随机整数
}

let subscription1 = deferredPublisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

let subscription2 = deferredPublisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

// 输出示例:
// Subscriber 1 received: 42
// Subscriber 2 received: 17
```

在这个示例中，每次新的订阅都会生成一个新的随机整数。`deferredPublisher` 在订阅时会执行闭包，生成 `Just` 发布者。

#### 应用场景

`Deferred` 特别适合于以下场景：

1. **动态数据**：当数据源在每次订阅时都可能不同，例如从网络获取数据或从数据库查询。
2. **条件创建**：根据某些条件决定要创建的 `Publisher` 类型，比如在不同条件下返回不同的数据流。
3. **延迟执行**：希望在订阅时才执行某些计算或获取数据，避免在创建时进行开销。

#### 例子：条件创建

假设我们希望根据用户的权限动态创建不同的 `Publisher`。可以使用 `Deferred` 来实现这个需求：

```swift
import Combine

enum UserPermission {
    case admin
    case guest
}

func getData(for permission: UserPermission) -> AnyPublisher<String, Never> {
    return Deferred {
        switch permission {
        case .admin:
            return Just("Admin data").eraseToAnyPublisher()
        case .guest:
            return Just("Guest data").eraseToAnyPublisher()
        }
    }
}

let permission: UserPermission = .admin

let subscription = getData(for: permission)
    .sink { value in
        print("Received: \(value)")
    }

// 输出: Received: Admin data
```

在这个例子中，`getData` 函数会根据传入的权限动态创建一个不同的 `Publisher`，而且在每次订阅时才会执行该逻辑。

#### 与其他 `Publisher` 的结合

`Deferred` 可以与其他 `Publisher` 和操作符结合使用，形成复杂的数据流。例如，你可以将 `Deferred` 与 `flatMap` 结合使用，以便在处理异步数据流时动态生成 `Publisher`。

```swift
let permissions = [UserPermission.admin, UserPermission.guest]

let subscriptions = permissions.publisher
    .flatMap { permission in
        getData(for: permission)
    }
    .sink { value in
        print("FlatMap received: \(value)")
    }

// 输出:
// FlatMap received: Admin data
// FlatMap received: Guest data
```

#### 总结

* `Deferred` 是 `Combine` 中用于延迟创建 `Publisher` 的强大工具。
* 它适合用于需要在每次订阅时动态生成数据流的场景，比如动态条件、懒加载等。
* `Deferred` 可以与其他 `Combine` 操作符结合使用，提供更大的灵活性和可重用性。

通过使用 `Deferred`，你可以在构建响应式应用程序时，更加灵活地处理数据流，从而增强应用的性能和响应性。
