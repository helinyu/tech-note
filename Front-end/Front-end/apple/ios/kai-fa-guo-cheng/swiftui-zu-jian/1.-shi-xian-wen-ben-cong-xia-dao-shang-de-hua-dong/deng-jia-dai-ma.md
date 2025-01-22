# 等价代码

```

import SwiftUI 
import Combine
struct WATimerDownToTopView: View {
 var questions: [String] = []

// 当前显示的问题索引
@State private var currentIndex = 0

// 用于存储订阅的 Cancellable 对象
@State private var cancellable: AnyCancellable?

var body: some View {
    VStack {
        if !questions.isEmpty {
            ZStack {
                ForEach(0..<questions.count, id: \.self) { index in
                    if index == currentIndex {
                        Text(questions[index])
                            .font(.largeTitle)
                            .padding()
                            .transition(.asymmetric(
                                insertion: .move(edge: .bottom), // 进入时从底部滑入
                                removal: .move(edge: .top)    // 退出时向顶部滑出
                            ))
                            .animation(.easeInOut(duration: 0.5), value: currentIndex) // 动画效果
                    }
                }
            }
            .frame(maxHeight: .infinity) // 修正：使用 maxHeight 而不是 height
            .background(Color.red)
            .clipped()
        }
    }
    .onAppear {
        // 在视图出现时开始订阅定时器
        cancellable = Timer.publish(every: 3, on: .main, in: .common)
            .autoconnect()
            .sink { _ in
                print("lt -- 内容处理的效果")
                if questions.count <= 1 { return }
                nextQuestion()
            }
    }
    .onDisappear {
        // 在视图消失时取消订阅
        cancellable?.cancel()
    }
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
