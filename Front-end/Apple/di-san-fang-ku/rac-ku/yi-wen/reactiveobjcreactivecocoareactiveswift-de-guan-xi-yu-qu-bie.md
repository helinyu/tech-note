# ReactiveObjC、ReactiveCocoa、ReactiveSwift的关系与区别

**ReactiveObjC**、**ReactiveCocoa** 和 **ReactiveSwift** 都属于响应式编程框架，最早都源于 ReactiveCocoa 项目，但随着语言的发展和需求的分化，它们分别演变成了独立的库。以下是它们的关系与区别：

#### 1. **关系**

* **ReactiveCocoa** 是最早的框架，是基于 GitHub 的响应式编程框架，最初支持 Objective-C 语言。它帮助开发者用响应式编程方式处理数据流和异步事件。
* 随着 Swift 的引入，**ReactiveCocoa** 的开发团队决定将 Objective-C 部分剥离，创建了 **ReactiveObjC**，用于继续支持 Objective-C 项目。
* 同时，**ReactiveCocoa** 项目本身转向 Swift 实现，但又进一步演化出了一个专门为 Swift 设计的库，即 **ReactiveSwift**，用于支持更纯粹的响应式 Swift 编程。
* 目前的结构是：**ReactiveObjC** 专门支持 Objective-C 项目，**ReactiveSwift** 专门支持 Swift 项目，而 **ReactiveCocoa** 则成为一个组合库，依赖于 ReactiveSwift，为 UIKit 或 AppKit 提供更高层的 Swift API 绑定。

#### 2. **区别**

| 特性       | ReactiveObjC        | ReactiveCocoa         | ReactiveSwift      |
| -------- | ------------------- | --------------------- | ------------------ |
| **支持语言** | Objective-C         | Swift                 | Swift              |
| **设计用途** | Objective-C 项目响应式编程 | UIKit/AppKit 层的响应式绑定  | Swift 项目中的底层响应式编程  |
| **主要功能** | 提供基础的响应式 API        | 提供 Swift 中 UI 层的响应式绑定 | 提供核心的响应式编程 API     |
| **代码复用** | 独立实现                | 依赖 ReactiveSwift      | 无需依赖其他库            |
| **使用场景** | 维护 Objective-C 旧项目  | 适用于需要 UI 绑定的 Swift 项目 | 适用于纯粹的响应式 Swift 项目 |

#### 3. **使用建议**

* **ReactiveObjC**：如果你有老的 Objective-C 项目或者项目中包含大量 Objective-C 代码，可以使用 ReactiveObjC 来保持对原有代码的兼容。
* **ReactiveCocoa**：对于以 Swift 为主的项目，可以选择 ReactiveCocoa。它使用了 ReactiveSwift 提供底层响应式 API，并额外提供了 UI 绑定的工具，使 Swift 项目中的 UIKit 或 AppKit 更易于实现响应式编程。
* **ReactiveSwift**：如果你在 Swift 项目中只需要核心的响应式编程功能（例如数据流处理，不涉及 UI 绑定），ReactiveSwift 是更轻量的选择。
