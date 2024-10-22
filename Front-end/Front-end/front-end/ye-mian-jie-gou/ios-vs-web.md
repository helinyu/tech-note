# iOS vs Web

在 Web 开发中，DOM (Document Object Model) 是页面的基础，它以树形结构的形式呈现 HTML 元素之间的父子关系。每个 HTML 标签、属性、文本内容都在这棵 DOM 树中作为一个节点。

在 iOS 中，页面结构同样采用树形结构，这个结构主要由 **UIView** 组成。所有的 UI 组件，如按钮 (UIButton)、标签 (UILabel)、图片视图 (UIImageView) 等，都是 **UIView** 的子类。整个 iOS 界面结构中，最顶层的是 **UIWindow**，它是其他视图的根节点。

#### 对比

1. **结构组成**
   * **DOM 树 (Web)**: 由 HTML 元素节点构成，节点类型包括元素节点、属性节点和文本节点等。
   * **iOS 视图树**: 由视图 (UIView) 组成，每个视图都有子视图 (subviews)，视图层次的顶端是 **UIWindow**。
2. **层次关系**
   * **DOM 树**: 各个 HTML 元素（如 `div`、`p`、`span`）之间有嵌套、父子关系。例如，`<div>` 可以包含多个 `<p>` 元素。
   * **UIView 树 (iOS)**: 类似于 DOM 树，`UIView` 也有层次结构。父视图可以包含多个子视图，每个子视图可以继续嵌套子视图。
3. **渲染机制**
   * **DOM 树 (Web)**: 通过浏览器渲染引擎（如 Chrome 的 Blink）来解析和渲染 HTML 结构，并使用 CSS 对其样式化。
   * **UIView 树 (iOS)**: iOS 通过 **Core Animation** 和 **QuartzCore** 渲染视图层次，确保视图树正确显示。
4. **事件处理**
   * **DOM 树 (Web)**: 事件通过事件冒泡和捕获机制沿着 DOM 树传播。点击或其他交互从子节点向父节点传播或反向传播。
   * **UIView 树 (iOS)**: iOS 采用 **Responder Chain** 来处理用户交互，事件在视图树中传播，比如手势触发从子视图传递到父视图，直到被某个视图处理。

#### 总结

Web 和 iOS 都采用树形结构来组织和管理页面元素或视图，主要区别在于 DOM 树用来表示文档结构，UIView 树则管理 UI 组件。
