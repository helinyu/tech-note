# 手动管理Combine中的Timer

使用 Combine 的 Timer 时，如果你希望手动管理它的启动和停止（而不是依赖 autoconnect()），可以通过以下步骤实现。手动管理的主要目的是更灵活地控制 Timer 的生命周期，例如在特定条件下启动或停止定时器。

***

#### 1. \*\*手动管理 Timer 的关键点\*\* <a href="#drxk-1737557047426" id="drxk-1737557047426"></a>

* \*\*使用 ConnectablePublisher\*\*：Combine 的 Timer.publish 返回的是一个 ConnectablePublisher，它不会自动启动，需要手动调用 connect() 来启动。
* \*\*存储 Cancellable\*\*：通过存储 connect() 返回的 Cancellable，你可以在需要时取消定时器。
* \*\*启动和停止\*\*：在适当的时机调用 connect() 和 cancel() 来控制定时器的启动和停止。

***

#### 2. \*\*手动管理 Timer 的步骤\*\* <a href="#edms-1737557047435" id="edms-1737557047435"></a>

以下是手动管理 Combine Timer 的完整步骤：

**（1）创建 Timer.TimerPublisher**

使用 Timer.publish 创建一个 Timer.TimerPublisher，但不要调用 autoconnect()。

**（2）存储 Cancellable**

调用 connect() 方法启动定时器，并存储返回的 Cancellable，以便后续取消。

**（3）在适当的时机启动和停止**

在需要的地方调用 connect() 和 cancel() 来控制定时器的启动和停止。

***

#### 3. \*\*示例代码\*\* <a href="#j0jt-1737557047452" id="j0jt-1737557047452"></a>

以下是一个手动管理 Combine Timer 的完整示例：

```
import SwiftUI
import Combine

struct ManualTimerView: View {
    @State private var currentTime = Date()
    @State private var timerCancellable: Cancellable? = nil

    // 创建 Timer.TimerPublisher
    let timerPublisher = Timer.publish(every: 1, on: .main, in: .common)

    var body: some View {
        VStack {
            Text("Current time: \(currentTime)")
                .font(.largeTitle)
                .padding()

            HStack {
                Button("Start Timer") {
                    startTimer()
                }
                .padding()
                .background(Color.blue)
                .foregroundColor(.white)
                .cornerRadius(10)

                Button("Stop Timer") {
                    stopTimer()
                }
                .padding()
                .background(Color.red)
                .foregroundColor(.white)
                .cornerRadius(10)
            }
        }
        .onReceive(timerPublisher) { time in
            currentTime = time
        }
        .onDisappear {
            stopTimer() // 视图消失时停止定时器
        }
    }

    // 启动定时器
    private func startTimer() {
        if timerCancellable == nil {
            timerCancellable = timerPublisher.connect() // 手动连接定时器
        }
    }

    // 停止定时器
    private func stopTimer() {
        timerCancellable?.cancel() // 取消定时器
        timerCancellable = nil
    }
}
```

***

#### 4. \*\*代码解析\*\* <a href="#tlkb-1737557047572" id="tlkb-1737557047572"></a>

**（1）Timer.publish**

* Timer.publish(every: 1, on: .main, in: .common) 创建了一个 Timer.TimerPublisher，但它不会自动启动。

**（2）connect()**

* 调用 timerPublisher.connect() 启动定时器，并返回一个 Cancellable。你需要存储这个 Cancellable，以便后续取消定时器。

**（3）cancel()**

* 调用 timerCancellable?.cancel() 停止定时器，并将 timerCancellable 置为 nil，释放资源。

**（4）onReceive**

* 使用 .onReceive(timerPublisher) 监听定时器的事件，并在每次触发时更新 currentTime。

**（5）onDisappear**

* 在视图消失时调用 stopTimer()，确保定时器被正确停止，避免内存泄漏。

***

#### 5. \*\*手动管理的优点\*\* <a href="#id-8z7a-1737557047596" id="id-8z7a-1737557047596"></a>

* \*\*更灵活的控制\*\*：你可以在任意时机启动和停止定时器，而不是依赖 autoconnect() 的自动行为。
* \*\*避免不必要的触发\*\*：在不需要定时器时（例如视图消失时），可以立即停止它，节省资源。
* \*\*适合复杂场景\*\*：例如，根据用户交互或应用状态动态控制定时器的启动和停止。

***

#### 6. \*\*注意事项\*\* <a href="#id-32wy-1737557047605" id="id-32wy-1737557047605"></a>

* \*\*避免重复启动\*\*：在调用 connect() 之前，检查 timerCancellable 是否为 nil，避免重复启动定时器。
* \*\*资源释放\*\*：在视图消失时（onDisappear）或不再需要定时器时，务必调用 cancel()，避免内存泄漏。
* \*\*线程安全\*\*：Timer 默认在主线程触发，因此可以直接在 .onReceive 中更新 UI。如果需要在后台线程执行任务，可以使用 DispatchQueue 或 Combine 的 receive(on:) 操作符。

***

#### 7. \*\*总结\*\* <a href="#ptm6-1737557047614" id="ptm6-1737557047614"></a>

手动管理 Combine 的 Timer 提供了更灵活的控制方式，适合需要动态启动和停止定时器的场景。通过 ConnectablePublisher 和 Cancellable，你可以精确控制定时器的生命周期，确保资源的高效使用。

