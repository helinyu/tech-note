# @State

`@State` 是 SwiftUI 中用于<mark style="color:red;">**管理视图状态**</mark>的属性包装器。它允许你在视图内部声明一个可变的状态变量，当这个<mark style="color:red;">变量的值改变时，视图会自动更新</mark>。

#### 基本用法：

1.  **导入 SwiftUI**：

    ```swift
    import SwiftUI
    ```
2.  **定义状态变量**： 使用 `@State` 声明一个变量：

    ```swift
    @State private var count: Int = 0
    ```
3.  **在视图中使用**： 可以在视图的 `body` 中使用这个状态变量：

    ```swift
    struct ContentView: View {
        @State private var count: Int = 0

        var body: some View {
            VStack {
                Text("Count: \(count)")
                Button("Increment") {
                    count += 1
                }
            }
            .padding()
        }
    }
    ```

#### 特点：

* **局部状态**：`@State` 变量是局部的，只在声明它的视图中有效。
* **自动更新**：当 `@State` 变量的值变化时，视图会自动重新渲染。
* **私有性**：`@State` 变量通常被声明为 `private`，以确保它只在该视图中被修改。

`@State` 是 SwiftUI 中管理简单状态的基础，适用于小型视图或局部状态的场景。
