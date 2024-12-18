# 实现两端的数据同步

当使用 UIViewRepresentable 或 UIViewControllerRepresentable 将 UIKit 组件集成到 SwiftUI 中时，确保 UIKit 端的数据变化能够同步到 SwiftUI 是一个常见的需求。为了实现这一点，你可以通过以下几种方法来处理：

#### 1. 使用 @Binding 和 Coordinator <a href="#id-1gox-1734531684810" id="id-1gox-1734531684810"></a>

这是最常见的方法之一。通过在 Coordinator 中监听 UIKit 端的数据变化，并将这些变化同步回 SwiftUI 视图的绑定属性。

**示例**

假设你有一个 UIKit 组件 WAHWDMP4PlayerOriginView，它会触发某些事件或改变内部状态。你需要将这些变化同步到 SwiftUI 的视图中。

```
struct WAHWDMP4PlayerView: UIViewRepresentable {
    @Binding var sources: [String]
    @Binding var playerState: PlayerState // 假设这是一个表示播放器状态的枚举

    func makeUIView(context: Context) -> WAHWDMP4PlayerOriginView {
        let playerView = WAHWDMP4PlayerOriginView()
        playerView.delegate = context.coordinator // 设置代理为 Coordinator
        return playerView
    }

    func updateUIView(_ uiView: WAHWDMP4PlayerOriginView, context: Context) {
        uiView.updateSources(sources: sources)
    }

    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }

    class Coordinator: NSObject, WAHWDMP4PlayerOriginViewDelegate {
        private var parent: WAHWDMP4PlayerView

        init(_ parent: WAHWDMP4PlayerView) {
            self.parent = parent
        }

        // 实现委托方法，处理数据变化
        func playerStateChanged(to newState: PlayerState) {
            parent.playerState = newState // 更新绑定属性
        }
    }
}

// 假设这是你的 UIKit 视图类
protocol WAHWDMP4PlayerOriginViewDelegate: AnyObject {
    func playerStateChanged(to newState: PlayerState)
}

class WAHWDMP4PlayerOriginView: UIView {
    weak var delegate: WAHWDMP4PlayerOriginViewDelegate?

    // 当播放器状态改变时调用此方法
    func changePlayerState(to newState: PlayerState) {
        // 更新内部状态逻辑
        delegate?.playerStateChanged(to: newState) // 通知 Coordinator
    }

    // 其他代码...
}
```

#### 2. 使用 @Published 和 ObservableObject <a href="#uxpg-1734531684919" id="uxpg-1734531684919"></a>

如果 UIKit 端的数据变化需要更复杂的处理，或者你有多个状态需要管理，可以考虑创建一个符合 ObservableObject 协议的对象，并使用 @Published 属性包装器来发布变化。

**示例**

```
class PlayerViewModel: ObservableObject {
    @Published var sources: [String] = []
    @Published var playerState: PlayerState = .idle

    // 其他逻辑...
}

struct WAHWDMP4PlayerView: UIViewRepresentable {
    @ObservedObject var viewModel: PlayerViewModel

    func makeUIView(context: Context) -> WAHWDMP4PlayerOriginView {
        let playerView = WAHWDMP4PlayerOriginView()
        playerView.delegate = context.coordinator
        return playerView
    }

    func updateUIView(_ uiView: WAHWDMP4PlayerOriginView, context: Context) {
        uiView.updateSources(sources: viewModel.sources)
    }

    func makeCoordinator() -> Coordinator {
        Coordinator(viewModel: viewModel)
    }

    class Coordinator: NSObject, WAHWDMP4PlayerOriginViewDelegate {
        private var viewModel: PlayerViewModel

        init(viewModel: PlayerViewModel) {
            self.viewModel = viewModel
        }

        func playerStateChanged(to newState: PlayerState) {
            viewModel.playerState = newState
        }
    }
}
```

#### 3. 使用 @State 和回调函数 <a href="#jum4-1734531685002" id="jum4-1734531685002"></a>

对于简单的数据同步，你也可以使用 @State 和回调函数来处理。

**示例**

```
struct WAHWDMP4PlayerView: UIViewRepresentable {
    @Binding var sources: [String]
    var onPlayerStateChanged: (PlayerState) -> Void

    func makeUIView(context: Context) -> WAHWDMP4PlayerOriginView {
        let playerView = WAHWDMP4PlayerOriginView()
        playerView.delegate = context.coordinator
        return playerView
    }

    func updateUIView(_ uiView: WAHWDMP4PlayerOriginView, context: Context) {
        uiView.updateSources(sources: sources)
    }

    func makeCoordinator() -> Coordinator {
        Coordinator(onPlayerStateChanged: onPlayerStateChanged)
    }

    class Coordinator: NSObject, WAHWDMP4PlayerOriginViewDelegate {
        private var onPlayerStateChanged: (PlayerState) -> Void

        init(onPlayerStateChanged: @escaping (PlayerState) -> Void) {
            self.onPlayerStateChanged = onPlayerStateChanged
        }

        func playerStateChanged(to newState: PlayerState) {
            onPlayerStateChanged(newState)
        }
    }
}

// 在 SwiftUI 视图中使用
struct ContentView: View {
    @State private var playerState: PlayerState = .idle

    var body: some View {
        VStack {
            WAHWDMP4PlayerView(sources: $sources, onPlayerStateChanged: { newState in
                self.playerState = newState
            })
            Text("Current State: \(playerState.rawValue)")
        }
    }
}
```

#### 关键点总结 <a href="#nmxu-1734531685100" id="nmxu-1734531685100"></a>

* \*\*@Binding\*\*：用于简单地将 UIKit 端的数据变化同步回 SwiftUI 视图。
* \*\*Coordinator\*\*：作为桥梁，处理事件和状态变化，并将其传递给 SwiftUI 视图。
* \*\*@Published 和 ObservableObject\*\*：用于管理更复杂的状态变化，确保所有相关视图都能响应这些变化。
* \*\*回调函数\*\*：对于简单的场景，可以直接使用回调函数来处理状态变化。

选择哪种方法取决于你的具体需求和应用的复杂度。通常，Coordinator 结合 @Binding 或 ObservableObject 是最常用且灵活的方法。
