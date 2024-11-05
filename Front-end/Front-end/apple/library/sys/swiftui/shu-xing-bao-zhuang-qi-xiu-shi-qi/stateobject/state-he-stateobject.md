# @State 和 @StateObject

`@State` 和 `@StateObject` 都是 SwiftUI 中用于管理和存储视图状态的属性包装器，但它们适用于不同的场景。以下是它们的详细对比：

| 特性         | @State                                      | @StateObject                                         |
| ---------- | ------------------------------------------- | ---------------------------------------------------- |
| **主要用途**   | 用于在视图内存储轻量级、简单的值                            | 用于在视图内存储可观察对象（`ObservableObject`）                    |
| **适用对象**   | 轻量级值类型（如 `Int`、`String` 等基本数据类型）            | 自定义的类对象，通常符合 `ObservableObject` 协议                   |
| **数据生命周期** | 由 SwiftUI 自动管理，当视图被销毁时数据也被销毁                | 对象的生命周期由 SwiftUI 管理，确保视图销毁时对象不被重新创建                  |
| **作用范围**   | 适用于单个视图，不会跨越多个视图共享状态                        | 适用于复杂的模型，通常需要跨多个视图共享状态                               |
| **数据变化响应** | 数据变化时，SwiftUI 自动更新视图                        | `ObservableObject` 的属性变化会触发视图更新                      |
| **初始化方式**  | 在视图内部直接初始化，如 `@State private var count = 0` | 必须在视图的初始阶段使用 `@StateObject` 初始化，避免重复创建               |
| **示例**     | `@State private var isOn: Bool = false`     | `@StateObject private var viewModel = MyViewModel()` |

#### 详细解释：

#### 1. **@State**：

* **用途**：用于存储**轻量级的、简单的值类型**，如布尔值、整数、字符串等。它是一种 SwiftUI 内部视图的状态，通常是视图内部的临时状态。
* **适用场景**：当状态不会被其他视图共享，仅在单个视图内变化时使用。
* **数据变化响应**：当使用 `@State` 标记的属性值发生变化时，SwiftUI 会自动重新渲染相应的视图。

**例子**：

```swift
struct CounterView: View {
    @State private var count = 0

    var body: some View {
        VStack {
            Text("Count: \(count)")
            Button("Increment") {
                count += 1
            }
        }
    }
}
```

#### 2. **@StateObject**：

* **用途**：用于存储**复杂对象**，这些对象通常遵循 `ObservableObject` 协议。`@StateObject` 适合管理生命周期长、需要跨视图共享的状态，比如视图模型（ViewModel）。
* **适用场景**：适用于需要在多个视图之间共享的复杂对象或模型，并且该对象会通过 `@Published` 进行属性的发布，进而触发视图的更新。
* **数据变化响应**：当 `@StateObject` 中的对象的属性通过 `@Published` 发生变化时，所有依赖该对象的视图都会被重新渲染。

**例子**：

```swift
class MyViewModel: ObservableObject {
    @Published var text: String = "Hello, World!"
}

struct ContentView: View {
    @StateObject private var viewModel = MyViewModel()

    var body: some View {
        VStack {
            Text(viewModel.text)
            Button("Change Text") {
                viewModel.text = "New Text"
            }
        }
    }
}
```

#### 总结：

| 特性           | @State                       | @StateObject                      |
| ------------ | ---------------------------- | --------------------------------- |
| **适用场景**     | 存储简单、轻量的值类型，如 `Bool`、`Int` 等 | 存储复杂对象，通常是 `ObservableObject` 类型  |
| **管理对象生命周期** | SwiftUI 内部管理数据生命周期，适合轻量级状态   | 适合管理生命周期较长的对象，如视图模型（ViewModel）    |
| **作用范围**     | 仅限单个视图内部使用                   | 适用于跨多个视图共享对象                      |
| **初始化方式**    | 直接初始化基本类型                    | 必须在视图初始时初始化并绑定 `ObservableObject` |

`@State` 适用于简单状态，而 `@StateObject` 更适合复杂对象状态管理。
