# 可包含控件

在SwiftUI中，`Form` 的内容可以包含多种控件，常见的有：

1. **TextField**：用于用户输入文本。
2. **SecureField**：用于输入敏感信息（如密码）。
3. **Toggle**：开关选项，适合启用或禁用某个设置。
4. **Picker**：下拉选择器，让用户从多个选项中选择。
5. **Slider**：用于选择数值范围。
6. **DatePicker**：选择日期和时间。
7. **Stepper**：用于增减数值。

你可以将这些控件组合在 `Form` 中，如下例所示：

```swift
Form {
    Section(header: Text("Account Info")) {
        TextField("Username", text: $username)
        SecureField("Password", text: $password)
    }
    
    Section(header: Text("Preferences")) {
        Toggle("Receive Notifications", isOn: $notificationsEnabled)
        Picker("Theme", selection: $selectedTheme) {
            Text("Light").tag(0)
            Text("Dark").tag(1)
        }
        Slider(value: $volume, in: 0...100, step: 1)
    }
}
```

这样可以清晰地组织输入项，提升用户体验。你有特定的控件想深入了解吗？
