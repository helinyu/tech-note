# RxSwift、ReactiveSwift 、Combine

下面是 RxSwift、ReactiveSwift 和 Combine 的关系与区别，以表格的形式列出：

| 特性        | RxSwift                            | ReactiveSwift                           | Combine                           |
| --------- | ---------------------------------- | --------------------------------------- | --------------------------------- |
| **起源**    | 基于 Rx 标准 (Reactive Extensions)     | 基于 ReactiveCocoa，原生 Swift 实现            | Apple 官方框架，iOS 13 及以上版本引入         |
| **支持语言**  | Swift                              | Swift                                   | Swift                             |
| **核心类型**  | `Observable`                       | `Signal` 和 `SignalProducer`             | `Publisher` 和 `Subscriber`        |
| **线程调度**  | 使用 `Schedulers` 控制线程               | 使用 `Scheduler` 控制线程                     | 内置 `DispatchQueue` 和 `RunLoop`    |
| **异步流**   | `Observable` 管理事件流                 | `Signal` 用于即时事件，`SignalProducer` 用于惰性计算 | `Publisher` 生成异步流，`Subscriber` 处理 |
| **操作符支持** | 丰富的 Rx 标准操作符                       | Swift 风格的操作符                            | 基于 Swift 的内置操作符                   |
| **平台支持**  | iOS、macOS、跨平台 Rx 家族成员              | iOS、macOS                               | iOS、macOS、watchOS、tvOS            |
| **典型应用**  | 跨平台响应式编程、具有 Rx 风格的 API             | 纯 Swift 项目，与 Swift 类型系统紧密结合             | 使用 Apple 框架的项目                    |
| **资源和社区** | Rx 社区支持广泛、资源丰富                     | Swift 社区支持，资源相对较少                       | Apple 官方支持，资源多且持续更新               |
| **常见扩展**  | `RxCocoa` 提供 UIKit 和 Foundation 支持 | 与 Swift 原生库兼容                           | 与 SwiftUI、UIKit 和 Foundation 深度整合 |
| **适用场景**  | 需要跨平台一致性、Rx 标准一致性                  | 偏向 Swift 开发，支持更高级别的流控制                  | 依赖 Apple 框架的项目及新特性                |

#### 总结：

* **RxSwift**：适合跨平台 Rx 系统，具有 Rx 风格的 API 和丰富的操作符。
* **ReactiveSwift**：适合 Swift 项目，与 Swift 语言深度集成，但社区资源少。
* **Combine**：Apple 官方框架，推荐在 iOS 13 及以上项目中使用，拥有更好的一体化支持与性能。
