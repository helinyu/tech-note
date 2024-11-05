# @EnvironmentObject vs @Environment

`@EnvironmentObject` 和 `@Environment` 都是 SwiftUI 中用于依赖注入的属性包装器，用于在视图树中传递数据，但它们有一些关键区别：

#### 1. **@EnvironmentObject**：

* **用途**：用于在视图树中共享一个**可观察对象**。该对象通常符合 `ObservableObject` 协议，可以包含多个属性。视图通过它可以响应数据的变化，自动更新 UI。
* **使用场景**：适用于多个视图都需要访问同一个数据模型，并且需要在数据改变时自动刷新这些视图。
* **初始化方式**：必须在视图的上层视图中通过 `.environmentObject(_:)` 方法将数据模型注入到视图环境中，否则会导致运行时崩溃。
*   **例子**：

    ```swift
    class AppData: ObservableObject {
        @Published var username: String = ""
    }

    struct ChildView: View {
        @EnvironmentObject var data: AppData

        var body: some View {
            Text("Username: \(data.username)")
        }
    }

    struct ParentView: View {
        var data = AppData()

        var body: some View {
            ChildView()
                .environmentObject(data)
        }
    }
    ```

#### 2. **@Environment**：

* **用途**：用于获取 SwiftUI 提供的系统环境值，如设备的 `colorScheme`、`locale`、`sizeCategory` 等。这些值通常是系统提供的全局属性，不能像 `@EnvironmentObject` 那样自定义。
* **使用场景**：适用于只需要读取系统环境中的属性值，而不需要绑定可观察对象。
* **初始化方式**：系统自动提供这些环境值，直接在视图中使用，无需手动注入。
*   **例子**：

    ```swift
    struct ContentView: View {
        @Environment(\.colorScheme) var colorScheme

        var body: some View {
            Text(colorScheme == .dark ? "Dark Mode" : "Light Mode")
        }
    }
    ```

#### 总结：

* **@EnvironmentObject**：适用于共享自定义数据模型，并且自动响应数据变化。
* **@Environment**：用于获取系统级别的环境数据，通常只用于读取环境值。

在 React 中，`@EnvironmentObject` 更类似于 `Context API`，因为它允许在组件树中共享状态，而 `@Environment` 则类似于获取一些全局的或环境相关的信息。
