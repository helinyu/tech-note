# Timer基于传统的实现和Combine的实现

在Combine 框架中的 Timer 和传统的 Timer（来自 Foundation 框架）在功能上是相似的，都是用于在指定时间间隔执行任务。然而，它们的实现方式和使用场景有一些关键区别，尤其是在与 SwiftUI 和 Combine 的响应式编程模型结合时。

***

#### 1. \*\*传统 Timer\*\* <a href="#new7-1737556198936" id="new7-1737556198936"></a>

传统的 Timer 是 Foundation 框架中的类，通常通过以下方式创建和使用：

```
let timer = Timer.scheduledTimer(withTimeInterval: 3, repeats: true) { timer in
    print("Timer fired!")
}
```

**特点：**

* \*\*基于闭包或目标-动作模式\*\*：通过闭包或目标-动作模式来处理定时器的触发事件。
* \*\*手动管理\*\*：需要手动启动、停止和释放定时器（通过 invalidate()）。
* \*\*运行循环（RunLoop）依赖\*\*：定时器需要添加到特定的 RunLoop 中（默认是主运行循环）。
* \*\*非响应式\*\*：传统 Timer 不是响应式的，无法直接与 Combine 的发布者-订阅者模型集成。

**缺点：**

* \*\*生命周期管理复杂\*\*：在 SwiftUI 中，需要手动管理定时器的启动和停止（例如在 onAppear 和 onDisappear 中）。
* \*\*容易导致内存泄漏\*\*：如果忘记调用 invalidate()，定时器可能会一直持有对象，导致内存泄漏。

***

#### 2. \*\*Combine 中的 Timer\*\* <a href="#uldb-1737556198966" id="uldb-1737556198966"></a>

Combine 框架提供了一个基于发布者（Publisher）的 Timer，可以通过 Timer.publish 创建：

```
let timerPublisher = Timer.publish(every: 3, on: .main, in: .common).autoconnect()
```

**特点：**

* \*\*基于发布者-订阅者模型\*\*：Timer 是一个发布者（Publisher），可以通过 Combine 的 sink 或 assign 订阅其事件。
* \*\*自动管理\*\*：使用 autoconnect() 可以自动启动定时器，或者手动通过 connect() 控制。
* \*\*与 SwiftUI 集成更好\*\*：Combine 的 Timer 可以直接与 SwiftUI 的 onReceive 修饰符结合使用，简化了代码。
* \*\*响应式编程\*\*：Combine 的 Timer 是响应式的，可以与其他 Combine 操作符（如 map、filter 等）结合使用。

**示例：**

```
import SwiftUI
import Combine

struct TimerView: View {
    @State private var currentTime = Date()

    let timerPublisher = Timer.publish(every: 1, on: .main, in: .common).autoconnect()

    var body: some View {
        Text("Current time: \(currentTime)")
            .onReceive(timerPublisher) { time in
                currentTime = time
            }
    }
}
```

**优点：**

* \*\*简化生命周期管理\*\*：Combine 的 Timer 可以自动管理启动和停止（通过 autoconnect()），也可以手动控制。
* \*\*与 SwiftUI 无缝集成\*\*：通过 onReceive 可以直接订阅定时器事件，无需手动管理。
* \*\*更强大的功能\*\*：Combine 的 Timer 可以与其他 Combine 操作符结合，实现更复杂的逻辑。

***

#### 3. \*\*主要区别\*\* <a href="#ifmt-1737556199030" id="ifmt-1737556199030"></a>

| 特性           | 传统 Timer                     | Combine Timer         |
| ------------ | ---------------------------- | --------------------- |
| 编程模型         | 基于闭包或目标-动作模式                 | 基于发布者-订阅者模型           |
| 生命周期管理       | 需要手动启动和停止（invalidate()）      | 自动管理（autoconnect()）   |
| 与 SwiftUI 集成 | 需要手动管理（onAppear/onDisappear） | 直接通过onReceive订阅       |
| 响应式支持        | 不支持                          | 支持，可与其他 Combine 操作符结合 |
| 运行循环依赖       | 需要添加到RunLoop                 | 自动运行在主线程的RunLoop      |
| 内存管理         | 容易导致内存泄漏                     | 更安全，自动释放              |

***

#### 4. \*\*何时使用哪种 Timer？\*\* <a href="#id-3cck-1737556199130" id="id-3cck-1737556199130"></a>

* 使用传统 Timer：
*
  * 如果你不需要与 Combine 或 SwiftUI 集成。
  * 如果你需要更细粒度的控制（例如将定时器添加到特定的 RunLoop）。
  * 如果你在非 SwiftUI 项目中使用（例如 UIKit 或 AppKit）。
* 使用 Combine Timer：
*
  * 如果你在 SwiftUI 或 Combine 项目中使用。
  * 如果你希望简化定时器的生命周期管理。
  * 如果你需要与其他 Combine 操作符结合使用（例如 map、filter 等）。

***

#### 总结 <a href="#akhd-1737556199150" id="akhd-1737556199150"></a>

Combine 的 Timer 更适合现代 SwiftUI 和响应式编程模型，提供了更简洁、更安全的 API。传统 Timer 则更适合需要手动控制的场景。根据你的项目需求选择合适的实现方式即可。



{% hint style="info" %}
总结：&#x20;

1） 也就是如果我们使用了SWiftUI， 就使用Combine的方式。&#x20;

2）onReceive 这个东西，只要拿到类似timer的变量，就可以订阅这个变量。

3）注意避免重复订阅，&#x20;

4）


{% endhint %}
