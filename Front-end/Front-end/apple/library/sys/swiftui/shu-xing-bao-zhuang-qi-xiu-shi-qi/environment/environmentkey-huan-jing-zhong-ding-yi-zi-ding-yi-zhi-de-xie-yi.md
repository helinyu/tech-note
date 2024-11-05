# EnvironmentKey(环境中定义自定义值的协议)

在 SwiftUI 中，`EnvironmentKey` 是用于在环境中定义自定义值的协议。通过实现 `EnvironmentKey` 协议，你可以为你的应用程序或视图层次结构提供全局可访问的共享值。

每个 `EnvironmentKey` 必须定义一个默认值，并且 SwiftUI 会通过环境为你管理这些值。

#### 定义 `EnvironmentKey`

1. 首先创建一个结构体或类来实现 `EnvironmentKey` 协议。
2. 在这个结构体中，定义一个 `defaultValue` 静态属性，它代表这个键的默认值。
3. 使用 `@Environment` 属性包装器，在视图中获取和使用这个自定义的环境值。

#### 示例

```swift
import SwiftUI

// 自定义一个环境键
struct CustomTitleKey: EnvironmentKey {
    static let defaultValue: String = "默认标题"
}

// 扩展 EnvironmentValues 来添加自定义键
extension EnvironmentValues {
    var customTitle: String {
        get { self[CustomTitleKey.self] }
        set { self[CustomTitleKey.self] = newValue }
    }
}

// 使用自定义的 EnvironmentKey
struct ContentView: View {
    @Environment(\.customTitle) var title

    var body: some View {
        Text(title)
    }
}

// 设置环境值
struct ParentView: View {
    var body: some View {
        ContentView()
            .environment(\.customTitle, "自定义标题")
    }
}
```

#### 关键点

1. `EnvironmentKey` 协议的作用是定义一个键，这个键可以被用来在视图树中存储和访问数据。
2. `EnvironmentValues` 是一组键值对，存储所有的环境键及其值。
3. `@Environment` 属性包装器允许你在视图中轻松访问环境中的某个键的值。

通过自定义 `EnvironmentKey`，你可以灵活地管理应用中不同视图之间共享的数据。
