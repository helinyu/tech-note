# Form

在 SwiftUI 中，`Form` 是一个用于组织和显示<mark style="color:red;">输入控件的容器</mark>，具有一些重要的属性和特性。以下是 `Form` 的一些关键属性和功能：

#### 主要属性和特性：

1.  **Sections**：

    * 可以使用 `Section` 来将表单中的控件分组，并添加标题或说明。每个 `Section` 可以包含一个或多个控件。

    ```swift
    Form {
        Section(header: Text("Account Info")) {
            // 控件
        }
    }
    ```
2. **Scrollability**：
   * `Form` 自动支持滚动，适合长表单。用户可以轻松浏览输入项。
3. **Styling**：
   * `Form` 会自动应用系统样式，确保输入控件的一致外观。
4.  **Editing Mode**：

    * 可以使用 `@State` 或 `@Binding` 属性包装器来跟踪用户输入，并在需要时更新状态。

    ```swift
    @State private var name: String = ""
    ```
5. **Validation**：
   * 可以在表单控件中实现简单的输入验证逻辑，例如检查输入的有效性。
6. **Buttons**：
   * 可以在表单中添加 `Button`，用于提交数据或执行操作。
7. **Custom Views**：
   * `Form` 可以包含自定义视图，使得输入控件可以更灵活。

#### 示例：

```swift
Form {
    Section(header: Text("Personal Information")) {
        TextField("Name", text: $name)
        SecureField("Password", text: $password)
    }
    
    Section {
        Button("Submit") {
            // 提交逻辑
        }
    }
}
```

通过使用 `Form`，你可以有效地组织用户输入，提升用户体验。
