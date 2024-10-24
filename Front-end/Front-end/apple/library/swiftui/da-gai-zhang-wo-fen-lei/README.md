# 内容范畴

官方地址： [https://developer.apple.com/documentation/swiftui](https://developer.apple.com/documentation/swiftui)

{% hint style="info" %}
官方提供的范畴：

1、App structure

2、Data and storage

3、Views

4、View layout

5、Event handling
{% endhint %}

SwiftUI 官方提供的范畴可以帮助开发者全面理解如何使用该框架构建用户界面。以下是每个范畴的具体内容：

#### 1. **App Structure**

* **`@main` 属性**：标识应用的入口点。
* **应用的生命周期**：管理应用状态和生命周期事件（如 `onAppear`、`onDisappear`）。
* **`Scene`**：管理应用的不同视图场景，可以是窗口或视图组。
* **`App` 协议**：定义应用的主要结构和行为。

#### 2. **Data and Storage**

* **状态管理**：
  * **`@State`**：用于在视图内部管理状态。
  * **`@Binding`**：用于在视图之间共享状态。
  * **`@ObservedObject`** 和 **`@StateObject`**：用于管理复杂的状态，依赖于遵循 `ObservableObject` 协议的模型。
* **数据持久化**：
  * 使用 `UserDefaults` 或其他数据存储方法（如 Core Data、文件存储）来持久化数据。
* **异步数据处理**：支持通过 Combine 或 Swift Concurrency 处理异步数据加载。

#### 3. **Views**

* **基本视图**：
  * **`Text`**、**`Image`**、**`Button`**、**`TextField`**、**`SecureField`**、**`Toggle`**、**`Slider`**、**`Picker`** 等。
* **组合视图**：使用容器视图（如 `HStack`、`VStack`、`ZStack`、`List`、`ScrollView` 等）组合多个视图。
* **自定义视图**：创建自定义视图组件，通过封装复用 UI 元素。

#### 4. **View Layout**

* **布局修饰符**：如 `frame`、`padding`、`background`、`cornerRadius` 等，修改视图的外观和布局。
* **对齐与间距**：使用 `alignment` 和 `spacing` 来控制视图的对齐和间距。
* **响应式布局**：使用 `GeometryReader` 和 `ViewModifier` 实现灵活的布局适应不同屏幕尺寸。

#### 5. **Event Handling**

* **手势识别**：使用 `.onTapGesture`、`.onLongPressGesture`、`.onDragGesture` 等修饰符处理用户手势。
* **按钮动作**：在 `Button` 中直接定义点击动作，使用闭包处理事件。
* **文本输入和表单**：处理用户输入的文本框和表单组件，包括 `TextField`、`SecureField` 和 `Form`。

#### 总结

这些范畴构成了 SwiftUI 的核心，涵盖了应用结构、数据管理、视图创建、布局设计和事件处理等方面。通过学习和理解这些内容，你可以更加高效地使用 SwiftUI 开发现代化的应用。

