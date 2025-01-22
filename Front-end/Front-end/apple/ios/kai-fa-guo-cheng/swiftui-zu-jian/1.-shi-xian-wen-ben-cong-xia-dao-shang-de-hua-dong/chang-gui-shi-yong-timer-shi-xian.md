# 常规使用Timer实现

如果你希望手动管理 Timer，而不是使用 Timer.publish 和 autoconnect()，可以通过以下步骤来实现：

#### 1. \*\*创建 Timer 实例\*\* <a href="#id-8y4g-1737556046611" id="id-8y4g-1737556046611"></a>

你需要手动创建一个 Timer 实例，并指定它的触发间隔、运行循环和模式。

#### 2. \*\*存储 Timer 实例\*\* <a href="#id-6eqt-1737556046615" id="id-6eqt-1737556046615"></a>

使用 @State 或 @StateObject 来存储 Timer 实例，以便在视图的生命周期中管理它。

#### 3. \*\*启动和停止 Timer\*\* <a href="#urh3-1737556046619" id="urh3-1737556046619"></a>

在适当的生命周期方法（如 onAppear 和 onDisappear）中启动和停止 Timer。

#### 4. \*\*处理 Timer 触发事件\*\* <a href="#id-6rfj-1737556046624" id="id-6rfj-1737556046624"></a>

使用 onReceive 或其他方式处理 Timer 触发的事件。

***

import SwiftUI import SwiftyFitsize

struct WATimerDownToTopView: View { var questions: \[String] = \[]

```
@State private var currentIndex = 0
@State private var timer: Timer? = nil // 手动管理 Timer

var body: some View {
    VStack {
        if !questions.isEmpty {
            ZStack {
                ForEach(0..<questions.count, id: \.self) { index in
                    if index == currentIndex {
                        Text(questions[index])
                            .systemBoldFont(size: 12~)
                            .foregroundColor(Color.white)
                            .padding(.horizontal, 0)
                            .transition(.asymmetric(
                                insertion: .move(edge: .bottom), // 进入时从底部滑入
                                removal: .move(edge: .top)       // 退出时向顶部滑出
                            ))
                            .animation(.easeInOut(duration: 0.5), value: currentIndex) // 动画效果
                    }
                }
            }
        }
    }
    .onAppear {
        startTimer() // 视图出现时启动 Timer
    }
    .onDisappear {
        stopTimer() // 视图消失时停止 Timer
    }
}

// 启动 Timer
private func startTimer() {
    timer = Timer.scheduledTimer(
        withTimeInterval: 3, // 每 3 秒触发一次
        repeats: true
    ) { _ in
        nextQuestion()
    }
}

// 停止 Timer
private func stopTimer() {
    timer?.invalidate() // 停止 Timer
    timer = nil
}

// 切换到下一个问题
private func nextQuestion() {
    withAnimation {
        currentIndex = (currentIndex + 1) % questions.count
    }
}

// 切换到上一个问题
private func previousQuestion() {
    withAnimation {
        currentIndex = (currentIndex - 1 + questions.count) % questions.count
    }
}
```

}

***

#### 优点 <a href="#hizc-1737556046805" id="hizc-1737556046805"></a>

* \*\*更灵活的控制\*\*：你可以完全控制 Timer 的启动和停止时机。
* \*\*避免不必要的触发\*\*：在视图消失时停止 Timer，避免后台继续运行。

***

#### 注意事项 <a href="#lyh0-1737556046812" id="lyh0-1737556046812"></a>

* \*\*内存管理\*\*：确保在视图消失时停止 Timer，否则可能导致内存泄漏。
* \*\*线程安全\*\*：Timer 默认在主线程运行，确保 UI 更新操作在主线程执行。
* \*\*性能优化\*\*：如果 Timer 的回调逻辑较复杂，可以考虑将耗时操作放到后台线程，避免阻塞主线程。
