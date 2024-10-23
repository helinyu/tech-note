# @AppStorage

<mark style="color:yellow;">`@AppStorage`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">是 SwiftUI 中用于</mark><mark style="color:purple;">**简化对 UserDefaults 的访问**</mark><mark style="color:yellow;">的属性包装器</mark><mark style="color:orange;">。</mark>

<mark style="color:orange;">它允许你将视图中的状态与 UserDefaults 中的存储值直接绑定。</mark>

#### 基本用法：

1.  **导入 SwiftUI**：

    ```swift
    import SwiftUI
    ```
2.  **定义属性**： 使用 `@AppStorage` 定义一个变量，并指定对应的 UserDefaults 键：

    ```swift
    @AppStorage("username") var username: String = "Guest"
    ```
3.  **在视图中使用**： 这个属性可以直接用在视图中，如下例：

    ```swift
    struct ContentView: View {
        @AppStorage("username") var username: String = "Guest"

        var body: some View {
            VStack {
                Text("Hello, \(username)!")
                TextField("Enter your name", text: $username)
                    .textFieldStyle(RoundedBorderTextFieldStyle())
                    .padding()
            }
            .padding()
        }
    }
    ```

#### 特点：

* **自动同步**：当你修改 `username` 的值时，UserDefaults 会自动更新；当应用重启时，`username` 会自动加载保存的值。
* **支持多种数据类型**：可以使用 `@AppStorage` 存储 `String`、`Int`、`Bool` 等类型的数据。

使用 `@AppStorage` 可以简化状态管理，减少手动读取和写入 UserDefaults 的代码。
