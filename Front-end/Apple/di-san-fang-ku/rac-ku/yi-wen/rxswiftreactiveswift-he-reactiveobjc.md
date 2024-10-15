# RxSwift、ReactiveSwift 和 ReactiveObjC

下面是 RxSwift、ReactiveSwift 和 ReactiveObjC 三者之间的关系与区别，以表格的形式列出：

| 特性        | RxSwift                            | ReactiveSwift                           | ReactiveObjC                     |
| --------- | ---------------------------------- | --------------------------------------- | -------------------------------- |
| **起源**    | 基于 Rx 标准 (Reactive Extensions)     | 基于 ReactiveCocoa，原生 Swift 实现            | 基于 Objective-C，ReactiveCocoa 的起点 |
| **支持语言**  | Swift                              | Swift                                   | Objective-C                      |
| **核心类型**  | `Observable`                       | `Signal` 和 `SignalProducer`             | `RACSignal`、`RACSequence`        |
| **线程调度**  | 使用 `Schedulers` 控制线程               | 使用 `Scheduler` 控制线程                     | 使用 `RACScheduler` 控制线程           |
| **异步流**   | 事件流通过 `Observable` 序列管理            | `Signal` 用于即时事件，`SignalProducer` 用于惰性计算 | `RACSignal` 用于事件流                |
| **操作符支持** | 支持 Rx 标准的丰富操作符                     | 提供更 Swift 化的操作符                         | 提供 ReactiveCocoa 风格的操作符          |
| **平台支持**  | iOS、macOS (跨平台 Rx 家族成员)            | iOS、macOS (主要 Swift 生态)                 | iOS、macOS (Objective-C 项目)       |
| **典型应用**  | 跨平台应用、响应式编程                        | 纯 Swift 项目，注重与 Swift 的兼容性               | 旧版项目、Objective-C 项目              |
| **社区和资源** | 受 Rx 家族支持，资源丰富                     | Swift 专用，资源相对较少                         | 社区较小，主要用于维护旧项目                   |
| **常见扩展**  | `RxCocoa` 用于 UIKit 和 Foundation 扩展 | 与 Swift 原生库兼容                           | 集成较少，配合其他 Cocoa 框架使用             |

总结来看，三者关系紧密但各有侧重点：

* **RxSwift** 和 **ReactiveSwift** 都源自响应式编程理念，前者基于 Rx 标准，后者则从 Objective-C 的 ReactiveCocoa 演化而来，适合 Swift。
* **ReactiveObjC** 则是较老的 Objective-C 版本，适合维护旧有 Objective-C 项目。
