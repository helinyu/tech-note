# NSWindowController

将 `NSWindowController` 与 SwiftUI 页面结合使用可以让你在 macOS 应用中更灵活地管理窗口和视图。下面是一个基本示例，展示如何将 `NSWindowController` 与 SwiftUI 结合：

#### 步骤 1: 创建 SwiftUI 视图

首先，创建一个简单的 SwiftUI 视图，例如 `AboutView`：

```swift
import SwiftUI

struct AboutView: View {
    var body: some View {
        VStack {
            Text("About this App")
                .font(.largeTitle)
                .padding()
            Text("This is a simple app using SwiftUI and NSWindowController.")
                .padding()
        }
    }
}
```

#### 步骤 2: 创建 NSWindowController

创建一个自定义的 `NSWindowController` 类，以管理窗口和视图：

```swift
import Cocoa
import SwiftUI

class AboutWindowController: NSWindowController {
    convenience init() {
        let contentView = AboutView()
        let hostingView = NSHostingView(rootView: contentView)

        let window = NSWindow(
            contentRect: NSRect(x: 0, y: 0, width: 400, height: 300),
            styleMask: [.titled, .closable, .resizable],
            backing: .buffered,
            defer: false
        )
        
        window.center()
        window.setFrameAutosaveName("About")
        window.contentView = hostingView
        
        self.init(window: window)
    }

    func showWindow(_ sender: Any?) {
        super.showWindow(sender)
    }
}
```

#### 步骤 3: 在应用中使用 NSWindowController

在你的主应用中，实例化并展示这个窗口控制器：

```swift
import SwiftUI

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

struct ContentView: View {
    var body: some View {
        VStack {
            Button("Show About") {
                let aboutWindowController = AboutWindowController()
                aboutWindowController.showWindow(nil)
            }
            .padding()
        }
    }
}
```

#### 说明

1. **创建 SwiftUI 视图**：在 `AboutView` 中定义要显示的内容。
2. **自定义 NSWindowController**：
   * 在 `AboutWindowController` 中创建一个窗口，设置其内容为 `NSHostingView`，并将 SwiftUI 视图传入。
   * `showWindow` 方法用于显示窗口。
3. **主应用**：在 `ContentView` 中创建一个按钮，点击后实例化并展示 `AboutWindowController`。

#### 注意事项

* 确保在主线程上更新 UI，通常在按钮的点击事件中调用 `showWindow` 是安全的。
* 根据需要调整窗口的大小和样式。
* 你可以在 `AboutWindowController` 中添加更多功能，比如窗口的关闭处理或其他自定义逻辑。

通过这种方式，你可以灵活地将传统的 Cocoa 应用程序与 SwiftUI 视图结合起来，利用两者的优点。
