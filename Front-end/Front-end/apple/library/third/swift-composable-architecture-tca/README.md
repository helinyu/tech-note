# swift-composable-architecture（TCA）



参考地址： [https://github.com/pointfreeco/swift-composable-architecture](https://github.com/pointfreeco/swift-composable-architecture)



`swift-composable-architecture` (TCA) 和 SwiftUI 之间的关系和区别可以理解为：**SwiftUI 是 UI 框架**，而 **TCA 是状态管理和架构框架**。它们的功能互补，但各自的关注点不同。

#### SwiftUI 的主要关注点

* **UI 框架**：SwiftUI 是苹果推出的用于构建用户界面的声明式框架，它专注于让开发者以简洁的方式创建 UI。开发者可以通过描述视图的当前状态来构建界面，而 SwiftUI 会自动处理界面的更新和重绘。
* **状态管理的内置机制**：SwiftUI 提供了简单的状态管理工具，如 `@State`、`@Binding`、`@ObservedObject`、`@EnvironmentObject` 等，这些可以帮助管理视图的状态和数据流。
* **面向 UI 的开发**：SwiftUI 的状态管理机制适合小型应用或简单组件的状态处理，因为它以视图层为中心进行状态绑定和刷新。

#### TCA 的主要关注点

* **架构框架**：TCA 是一个架构工具，主要关注的是如何**管理应用程序中的状态**，**处理业务逻辑**，以及如何通过组合模块来构建复杂应用。TCA 为 Swift 和 SwiftUI 提供了一个更严谨、模块化的架构。
* **集中式状态管理**：TCA 强调使用集中式的状态管理，所有状态变化通过 `Action` 和 `Reducer` 来驱动。相比 SwiftUI 的状态管理工具，TCA 更适合大型应用程序，特别是在涉及复杂状态和业务逻辑时，TCA 提供了更强大的可维护性和可测试性。
* **副作用管理**：TCA 通过 `Effect` 的概念将副作用（如网络请求、定时任务）与核心业务逻辑分离，确保业务逻辑可以通过纯函数来实现，这使得逻辑更容易测试和推理。
* **模块化和可组合性**：TCA 可以让开发者将应用拆分为多个小模块，每个模块都有自己的 `State`、`Action` 和 `Reducer`，然后可以组合这些模块来构建复杂的应用。

#### SwiftUI 和 TCA 的区别

1. **状态管理范围**：
   * **SwiftUI**：提供基本的状态管理工具（如 `@State`, `@Binding` 等），适合小型应用或简单的状态管理场景。
   * **TCA**：提供更强大的集中式状态管理工具，适合复杂的应用场景，特别是在涉及多个模块、复杂业务逻辑和副作用时，TCA 提供了更好的组织和管理方式。
2. **可测试性**：
   * **SwiftUI**：默认的状态管理工具不太容易进行单元测试，尤其是当副作用混入业务逻辑时，测试会变得更加复杂。
   * **TCA**：TCA 的设计天然支持测试，通过将业务逻辑与副作用分离，并使用纯函数和 `Effect`，使得测试业务逻辑非常简单和高效。
3. **架构复杂度**：
   * **SwiftUI**：适合小型或中型应用，默认的状态管理和架构非常简单且足够用，但对于复杂应用可能会不够灵活和清晰。
   * **TCA**：适合中型到大型应用，提供了更多的架构工具来帮助开发者保持项目的可维护性、可扩展性和可测试性。
4. **模块化与组合**：
   * **SwiftUI**：视图组合简单，但状态和逻辑的组合能力有限，尤其是当应用变得复杂时，状态管理和业务逻辑可能会分散在多个视图中，导致难以维护。
   * **TCA**：提供了模块化和组合机制，允许你将应用拆分为独立的模块，管理各自的状态和逻辑，然后组合它们。这种模式非常适合需要多团队协作或者需要扩展的应用。
5. **副作用管理**：
   * **SwiftUI**：副作用（如网络请求或定时器）通常会混合在视图或状态逻辑中，这可能会导致代码难以测试和维护。
   * **TCA**：TCA 强调将副作用与核心逻辑分离，通过 `Effect` 管理副作用，确保逻辑的纯净性和可测试性。

#### 结合使用

SwiftUI 和 TCA 之间并不是互相排斥的，**TCA 通常被用作 SwiftUI 应用的架构层**。SwiftUI 负责声明式构建界面，而 TCA 负责处理应用的状态管理、业务逻辑和副作用。

#### 什么时候使用 SwiftUI，什么时候使用 TCA？

* 如果你在构建一个**简单的应用**，并且状态和逻辑相对较简单，SwiftUI 内置的状态管理机制通常就足够了。
* 如果你在构建一个**复杂应用**，涉及到多个模块、复杂的状态逻辑、以及需要大量的单元测试，那么使用 TCA 来管理应用的状态和逻辑会是更好的选择。

#### 总结

* **SwiftUI**：UI 框架，适合声明式构建用户界面，并提供基本的状态管理工具。
* **TCA**：架构框架，专注于复杂应用中的状态管理、业务逻辑和副作用处理，适合更复杂的项目。

SwiftUI 可以与 TCA 结合使用，SwiftUI 处理视图层面，TCA 管理应用的状态和逻辑。