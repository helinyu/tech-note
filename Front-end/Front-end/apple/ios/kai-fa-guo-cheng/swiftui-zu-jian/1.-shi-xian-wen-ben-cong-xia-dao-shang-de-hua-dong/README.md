# 1. 实现文本从下到上的滑动

```
import SwiftUI
import SwiftyFitsize

// 未来再进行修改 ，适配更多内容
struct WATimerDownToTopView: View {
    var questions:[String] = []
    
    @State private var currentIndex = 0

    let timer = Timer.publish(every: 3, on: .main, in: .common).autoconnect()
    
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
                                    removal: .move(edge: .top)    // 退出时向d顶部部滑出
                                ))
                                .animation(.easeInOut(duration: 0.5), value: currentIndex) // 动画效果
                        }
                    }
                }
//                .background(Color.red)
//                .clipped()
            }
        }
        .onReceive(timer) { _ in
            if questions.count <= 1 { return }
            nextQuestion()
        }
    }
    
    private func nextQuestion() {
        withAnimation {
            currentIndex = (currentIndex + 1) % questions.count
        }
    }
    
    private func previousQuestion() {
        withAnimation {
            currentIndex = (currentIndex - 1 + questions.count) % questions.count
        }
    }
}
```

1. 定时器， Timer + Combine 【Publisher+Combine】
2. 动画 withAnimation 的的内容
3. transition转场的过程， .asymmetric的内容 。&#x20;

