# @Environment

`@Environment` 是 SwiftUI 中用于<mark style="color:red;">**访问环境值**</mark>的属性包装器。它允许你从视图的环境中获取信息，例如系统设置、用户界面风格、颜色方案等。这使得在不同层级的视图中共享和传递数据变得简单。

#### 基本用法：

1.  **导入 SwiftUI**：

    ```swift
    import SwiftUI
    ```
2.  **定义环境变量**： 使用 `@Environment` 声明一个变量，通常与系统预定义的环境值关联。例如，获取当前的颜色方案：

    ```swift
    @Environment(\.colorScheme) var colorScheme
    ```
3.  **在视图中使用**： 在视图中使用该环境变量：

    ```swift
    struct ContentView: View {
        @Environment(\.colorScheme) var colorScheme

        var body: some View {
            VStack {
                Text("Current color scheme: \(colorScheme == .dark ? "Dark" : "Light")")
            }
            .padding()
        }
    }
    ```

#### 特点：

* **环境值**：可以访问的环境值包括但不限于颜色方案、字体、显示尺寸等。
* **层次结构**：环境值是从视图层次结构中自动传递的，子视图可以访问父视图设置的环境值。
* **动态变化**：如果环境值在运行时发生变化（如用户更改主题），相关的视图会自动更新。

`@Environment` 适合用于需要依赖系统或上下文信息的场景，使得应用更加灵活和响应式。
