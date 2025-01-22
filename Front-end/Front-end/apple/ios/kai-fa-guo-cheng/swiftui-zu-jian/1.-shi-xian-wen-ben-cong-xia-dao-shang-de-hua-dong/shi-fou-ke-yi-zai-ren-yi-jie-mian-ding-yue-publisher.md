# 是否可以在任意界面订阅publisher？

可以在任意界面使用 .onReceive(timerPublisher) 来订阅 Combine 的 Timer 发布者\*\*。这是因为 .onReceive 是 SwiftUI 提供的一个修饰符，专门用于监听发布者（Publisher）发出的值，并在接收到新值时更新视图。不过，是否在任意界面使用 .onReceive(timerPublisher) 取决于你的具体需求和设计。以下是一些需要注意的事项：

***

#### 1. \*\*.onReceive 的使用场景\*\* <a href="#jz93-1737556795900" id="jz93-1737556795900"></a>

.onReceive 主要用于在 SwiftUI 视图中监听发布者（如 Combine 的 Timer、PassthroughSubject 等）发出的值。它非常适合以下场景：

* 定时更新 UI（例如倒计时、轮播图）。
* 监听外部数据源的变化（例如网络请求的结果）。
* 响应自定义发布者的事件。

***

#### 2. \*\*在任意界面使用的条件\*\* <a href="#ss7j-1737556795911" id="ss7j-1737556795911"></a>

虽然可以在任意界面使用 .onReceive(timerPublisher)，但需要注意以下几点：

**（1）\*\*Timer 的生命周期\*\***

* 如果你使用 Timer.publish(every:on:in).autoconnect()，定时器会在视图出现时自动启动，并在视图消失时自动停止。
* 如果你手动管理 Timer（例如通过 ConnectablePublisher 的 connect() 和 cancel()），需要确保在适当的时机启动和停止定时器，以避免资源浪费或内存泄漏。

**（2）\*\*性能影响\*\***

* 如果界面中订阅了多个 Timer，或者 Timer 的触发频率很高（例如每秒触发多次），可能会对性能产生影响。
* 确保 Timer 的回调逻辑尽量轻量，避免阻塞主线程。

**（3）\*\*界面消失时的处理\*\***

* 如果界面消失时不需要继续运行 Timer，可以使用 autoconnect() 或手动停止定时器。
* 如果界面消失时需要继续运行 Timer（例如在后台更新数据），需要确保定时器的生命周期与界面无关。

***

#### 3. \*\*示例：在多个界面中使用 .onReceive\*\* <a href="#fumh-1737556795935" id="fumh-1737556795935"></a>

以下是一个示例，展示了如何在多个界面中使用&#x20;

```
import SwiftUI
import Combine

struct ContentView: View {
    var body: some View {
        NavigationView {
            VStack {
                NavigationLink("Go to Timer View 1", destination: TimerView1())
                NavigationLink("Go to Timer View 2", destination: TimerView2())
            }
        }
    }
}

struct TimerView1: View {
    @State private var currentTime = Date()

    let timerPublisher = Timer.publish(every: 1, on: .main, in: .common).autoconnect()

    var body: some View {
        Text("Timer View 1: \(currentTime)")
            .onReceive(timerPublisher) { time in
                currentTime = time
            }
    }
}

struct TimerView2: View {
    @State private var count = 0

    let timerPublisher = Timer.publish(every: 2, on: .main, in: .common).autoconnect()

    var body: some View {
        Text("Timer View 2: \(count)")
            .onReceive(timerPublisher) { _ in
                count += 1
            }
    }
}
```



#### 4. \*\*注意事项\*\* <a href="#i4ui-1737556796024" id="i4ui-1737556796024"></a>

**（1）\*\*避免重复订阅\*\***

* 如果多个界面订阅了同一个 Timer 发布者，可能会导致重复触发。可以通过共享发布者（例如将 Timer 放在 ObservableObject 中）来避免这个问题。

**（2）\*\*界面消失时的行为\*\***

* 如果界面消失时不需要继续运行 Timer，可以使用 autoconnect()，它会自动管理定时器的生命周期。
* 如果界面消失时需要继续运行 Timer，可以将 Timer 放在一个全局对象（如 ObservableObject）中，并在多个界面中共享。

**（3）\*\*线程安全\*\***

* Timer 默认在主线程触发，因此可以直接在 .onReceive 中更新 UI。
* 如果需要在后台线程执行任务，可以使用 DispatchQueue 或 Combine 的 receive(on:) 操作符。

***

#### 5. \*\*共享 Timer 的示例\*\* <a href="#cfqr-1737556796043" id="cfqr-1737556796043"></a>

如果你希望在多个界面中共享同一个 Timer，可以将其放在 ObservableObject 中：

```
import SwiftUI
import Combine

class TimerManager: ObservableObject {
    @Published var currentTime = Date()
    private var timerPublisher: Timer.TimerPublisher
    private var cancellable: Cancellable?

    init() {
        timerPublisher = Timer.publish(every: 1, on: .main, in: .common)
        cancellable = timerPublisher.autoconnect().assign(to: \.currentTime, on: self)
    }
}

struct ContentView: View {
    @StateObject private var timerManager = TimerManager()

    var body: some View {
        NavigationView {
            VStack {
                NavigationLink("Go to Timer View 1", destination: TimerView1(timerManager: timerManager))
                NavigationLink("Go to Timer View 2", destination: TimerView2(timerManager: timerManager))
            }
        }
    }
}

struct TimerView1: View {
    @ObservedObject var timerManager: TimerManager

    var body: some View {
        Text("Timer View 1: \(timerManager.currentTime)")
    }
}

struct TimerView2: View {
    @ObservedObject var timerManager: TimerManager

    var body: some View {
        Text("Timer View 2: \(timerManager.currentTime)")
    }
}
// 这个结果，应该是定时器1s刷新UI + 1，显示有关的效果
```

***

#### 总结 <a href="#id-6wm0-1737556796137" id="id-6wm0-1737556796137"></a>

* \*\*可以在任意界面使用 .onReceive(timerPublisher)\*\*，但需要根据具体需求管理 Timer 的生命周期。
* 如果多个界面需要共享同一个 Timer，可以将其放在 ObservableObject 中。
* 注意性能问题和线程安全，确保 Timer 的使用不会对应用造成负面影响。



{% hint style="info" %}
总结：

1） onreceive 订阅publisher的内容，只要拿到就可以订阅到

2） Timer中使用AutoConnect页面显示就会启动， 页面小时就会消失

3）通过一个变量，共享timer
{% endhint %}
