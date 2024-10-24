# NavigationView、NavigationStack 和 NavigationSplitView

`NavigationView`、`NavigationStack` 和 `NavigationSplitView` 是 SwiftUI 中的三种导航组件，它们随着 SwiftUI 的发展在功能上逐步增强，提供了不同的导航体验和布局方式。下面是它们的详细对比：

#### 1. **NavigationView**

**主要特性：**

* **引入版本**：SwiftUI 初始版本（iOS 13）
* **功能**：提供一个简单的导航堆栈，允许通过 `NavigationLink` 在视图之间导航。
* **适用平台**：iOS、macOS、watchOS、tvOS。
* **导航控制**：相对简单，自动管理导航堆栈，推入或弹出视图。

**优缺点：**

* **优点**：
  * 简单易用，适合小型、单层次导航的应用。
  * 能够在 iOS 上显示导航栏，并支持返回、前进操作。
* **缺点**：
  * 对导航堆栈的控制能力有限，不支持灵活的状态管理。
  * 在多屏设备（如 iPad 或 macOS）上缺乏更高级的导航功能。
  * 自 iOS 16 起，已逐渐被 `NavigationStack` 和 `NavigationSplitView` 取代。

**示例：**

```swift
NavigationView {
    VStack {
        NavigationLink(destination: Text("Detail View")) {
            Text("Go to Detail")
        }
    }
    .navigationTitle("Home")
}
```

#### 2. **NavigationStack**

**主要特性：**

* **引入版本**：iOS 16、macOS 13
* **功能**：增强了对导航状态的控制，允许开发者显式管理导航堆栈，可以处理多个视图层次。
* **适用平台**：iOS、macOS。
* **状态管理**：可以将视图堆栈状态与 `Binding` 或 `State` 变量绑定，提供灵活的导航管理。

**优缺点：**

* **优点**：
  * 增强了导航状态管理，可以轻松访问和操控导航历史。
  * 提供了对导航堆栈的更精细控制，支持深层次的页面导航。
  * 适用于复杂的导航逻辑，实现响应式和动态导航行为。
* **缺点**：
  * 相比 `NavigationView`，稍微复杂一些，但提供了更高的灵活性。

**示例：**

```swift
@State private var path = [String]()

NavigationStack(path: $path) {
    VStack {
        Button("Go to Detail") {
            path.append("DetailView")
        }
    }
    .navigationDestination(for: String.self) { value in
        if value == "DetailView" {
            Text("Detail View")
        }
    }
    .navigationTitle("Home")
}
```

#### 3. **NavigationSplitView**

**主要特性：**

* **引入版本**：iOS 16、macOS 13
* **功能**：用于多列导航，支持分屏布局，适合 iPad 和 macOS 上的主从视图或复杂布局需求。
* **适用平台**：iPadOS、macOS。
* **分栏导航**：提供了多个列，适合同时展示侧边栏和主视图内容，非常适合大型屏幕应用。

**优缺点：**

* **优点**：
  * 支持多列导航布局，特别适合 iPad 和 macOS 上的分屏使用场景。
  * 提供同时展示多个视图的能力，用户可以在一个界面中浏览和操作多个视图。
  * 在较大屏幕设备上用户体验更好，且支持横屏下的复杂布局。
* **缺点**：
  * 主要针对大屏设备，不适用于 iPhone 等较小屏幕设备。

**示例：**

```swift
NavigationSplitView {
    List(0..<5) { index in
        NavigationLink("Item \(index)", value: index)
    }
} detail: { value in
    Text("Detail for item \(value)")
}
.navigationTitle("Items")
```

#### 对比总结

| 特性         | NavigationView         | NavigationStack  | NavigationSplitView    |
| ---------- | ---------------------- | ---------------- | ---------------------- |
| **引入版本**   | iOS 13                 | iOS 16           | iOS 16                 |
| **适用平台**   | iOS、macOS、tvOS、watchOS | iOS、macOS        | iPadOS、macOS           |
| **状态管理**   | 自动管理堆栈，状态管理较弱          | 支持显式堆栈管理，状态更灵活   | 支持多列视图，适合大屏设备          |
| **多层次导航**  | 支持但灵活性较差               | 强大的多层次导航支持       | 支持多列导航，尤其适合主从视图布局      |
| **典型用法**   | 简单导航，单页面导航             | 复杂导航逻辑，状态控制      | 适合大屏幕设备，如 iPad 和 macOS |
| **推荐使用场景** | 小型应用或简单导航              | 多层导航结构、需要状态管理的应用 | 多列布局，主从结构，适用于大屏设备      |
| **未来发展方向** | 逐渐被替代                  | 推荐用于现代应用         | 大屏设备上的最佳导航方案           |

#### 总结

* **`NavigationView`**：适合简单的导航结构，虽然目前仍然可以使用，但在 iOS 16 及更高版本中已逐步被替代。
* **`NavigationStack`**：是对 `NavigationView` 的改进，支持更灵活的导航堆栈管理，适合复杂的导航应用。
* **`NavigationSplitView`**：主要针对大屏设备，支持多列导航，非常适合主从结构和复杂布局的应用，尤其是 iPad 和 macOS。

在现代应用开发中，推荐优先使用 `NavigationStack` 和 `NavigationSplitView` 来替代 `NavigationView`，以利用其增强的功能和灵活性。
