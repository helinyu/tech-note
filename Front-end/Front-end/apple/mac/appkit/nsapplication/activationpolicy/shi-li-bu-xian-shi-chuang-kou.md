# 示例（不显示窗口）

确实，使用 `WindowGroup` 时，SwiftUI 默认会创建一个窗口。要完全不显示窗口，可以通过使用 `NSApplication` 的 `setActivationPolicy` 方法将应用的激活策略设置为 `.accessory`，这样可以确保应用在没有窗口的情况下运行。

下面是更新后的示例，展示如何实现这一点：

```swift
import SwiftUI

@main
struct StatusBarApp: App {
    @NSApplicationDelegateAdaptor(AppDelegate.self) var appDelegate

    var body: some Scene {
        // 不创建任何窗口
        EmptyScene()
    }
}

class AppDelegate: NSObject, NSApplicationDelegate {
    var statusItem: NSStatusItem?

    func applicationDidFinishLaunching(_ aNotification: Notification) {
        // 设置应用程序的激活策略为 accessory
        NSApplication.shared.setActivationPolicy(.accessory)

        // 创建状态栏项
        statusItem = NSStatusBar.system.statusItem(withLength: NSStatusItem.squareLength)

        if let button = statusItem?.button {
            button.image = NSImage(systemSymbolName: "star", accessibilityDescription: "Star")
            button.action = #selector(statusBarButtonClicked)
        }

        // 添加菜单
        let menu = NSMenu()
        menu.addItem(NSMenuItem(title: "Item 1", action: #selector(menuItemClicked), keyEquivalent: "n"))
        menu.addItem(NSMenuItem(title: "Quit", action: #selector(NSApp.terminate(_:)), keyEquivalent: "q"))
        statusItem?.menu = menu
    }

    @objc func statusBarButtonClicked() {
        // 响应点击状态栏图标的事件
        print("Status bar button clicked!")
    }

    @objc func menuItemClicked() {
        // 响应菜单项点击事件
        print("Menu item clicked!")
    }
}

struct EmptyScene: Scene {
    var body: some Scene {
        // 不创建任何窗口
        WindowGroup {
            EmptyView()
        }
    }
}
```

#### 关键点：

* **`NSApplication.shared.setActivationPolicy(.accessory)`**：在 `applicationDidFinishLaunching` 方法中设置应用程序的激活策略为 `.accessory`，这样就不会创建主窗口。
* **`EmptyScene`**：保持 Scene 的结构，确保不会创建实际的窗口。

这样，你的应用将在没有任何主窗口的情况下运行，并且只在状态栏中显示图标。
