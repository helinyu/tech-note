# SwiftUI更新历史

SwiftUI 是 Apple 于 2019 年推出的声明式 UI 框架，旨在简化用户界面开发。以下是 SwiftUI 各版本的更新历史概要：

***

#### **SwiftUI 1.0 (2019)**

**发布时间：2019 年 6 月（随 iOS 13, macOS Catalina, watchOS 6, tvOS 13）**

* **初次发布**：基于声明式语法构建 UI，替代 Interface Builder 和 UIKit 的部分功能。
* **核心功能**：
  * 使用`@State`、`@Binding`、`@Environment`等属性包装器管理状态和数据流。
  * 支持动态列表（`List`）、栈布局（`HStack`、`VStack`）和动画。
  * 支持与 UIKit、AppKit 互操作。
  * 引入了视图组合（`Group`）和修饰符链式调用。

***

#### **SwiftUI 2.0 (2020)**

**发布时间：2020 年 6 月（随 iOS 14, macOS Big Sur, watchOS 7, tvOS 14）**

* **新功能和改进**：
  * **新控件**：`ProgressView`、`ColorPicker`、`Label`。
  * 支持图表和新的列表样式（`InsetGroupedListStyle`）。
  * **App 架构**：提供`@App`协议替代`UIApplicationDelegate`，支持多窗口管理。
  * **图形支持**：支持小组件（Widgets）开发。
  * **手势改进**：更加灵活的手势合成和事件响应。
  * 引入 `@SceneStorage` 支持持久化小范围状态。

***

#### **SwiftUI 3.0 (2021)**

**发布时间：2021 年 6 月（随 iOS 15, macOS Monterey, watchOS 8, tvOS 15）**

* **新控件和布局**：
  * 支持异形屏幕适配（`Canvas`）。
  * 新增 `List` 的可拖拽分组。
  * 支持 `TextEditor` 定制化。
* **更强的状态管理**：
  * 新增`@FocusState`，支持键盘焦点管理。
* **增强可访问性**：
  * 动态类型调整和语音优化。
* 提供 `Refreshable` 功能以实现下拉刷新。

***

#### **SwiftUI 4.0 (2022)**

**发布时间：2022 年 6 月（随 iOS 16, macOS Ventura, watchOS 9, tvOS 16）**

* **更强的控件支持**：
  * 引入`Grid`布局，支持灵活网格设计。
  * 新增 `ShareLink` 和 `NavigationSplitView`。
  * 强化图形和绘制功能，支持 `Charts`。
* **导航改进**：
  * 全新的 `NavigationStack` 替代`NavigationView`，支持更强的可控性。
* **动画与动态更新**：
  * 改进`Lottie`式动画支持。
* 支持滚动视图自动对齐和分页（`scrollTargetBehavior`）。

***

#### **SwiftUI 5.0 (2023)**

**发布时间：2023 年 6 月（随 iOS 17, macOS Sonoma, watchOS 10, tvOS 17）**

* **新功能亮点**：
  * **透视导航**：新增 `Observable` 和更复杂的数据流管理。
  * **全屏视图**：支持新形式的全屏展示模式。
  * **自定义动画**：提供更强的动态交互支持。
  * **增强设计工具链**：在 Xcode 中的实时预览更高效。
  * 对交互式小部件（如 StandBy 和锁屏 Widgets）支持更完善。
