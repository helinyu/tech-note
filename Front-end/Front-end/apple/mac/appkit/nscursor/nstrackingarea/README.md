# NSTrackingArea

`NSTrackingArea` 是 macOS 中用于跟踪鼠标事件的类。它允许你定义一个矩形区域，以便在该区域内接收鼠标相关的事件（如进入、离开和移动事件）。以下是关于 `NSTrackingArea` 的详细内容：

#### 1. **初始化**

创建 `NSTrackingArea` 时，你需要指定矩形、选项、所有者和用户信息。以下是初始化方法的签名：

```swift
init(rect: NSRect, options: NSTrackingArea.Options, owner: AnyObject?, userInfo: [String: Any]?)
```

* **rect**: 跟踪区域的矩形框。
* **options**: 指定跟踪区域的行为选项。
* **owner**: 接收事件的对象（通常是视图）。
* **userInfo**: 可选的用户信息字典，包含额外的数据。

#### 2. **选项 (Options)**

`NSTrackingArea.Options` 是一个包含不同选项的结构体，用于定义跟踪区域的行为。常用的选项包括：

* **`mouseEntered`**: 监听鼠标进入该区域的事件。
* **`mouseExited`**: 监听鼠标离开该区域的事件。
* **`mouseMoved`**: 监听鼠标在该区域内移动的事件。
* **`activeInActiveApp`**: 仅在应用处于活动状态时激活跟踪区域。
* **`activeInKeyWindow`**: 仅在窗口为键窗口时激活跟踪区域。
* **`activeAlways`**: 始终激活跟踪区域，无论应用或窗口的状态。
* **`assumeInside`**: 假设鼠标当前在该区域内（在创建时触发相应事件）。
* **`inVisibleRect`**: 仅在可见区域内触发事件。

#### 3. **使用示例**

以下是一个简单的示例，展示如何在自定义视图中使用 `NSTrackingArea`：

```swift
import Cocoa

class CustomView: NSView {
    override init(frame frameRect: NSRect) {
        super.init(frame: frameRect)
        setupTrackingArea()
    }
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        setupTrackingArea()
    }
    
    private func setupTrackingArea() {
        let trackingArea = NSTrackingArea(
            rect: bounds,
            options: [.mouseEntered, .mouseExited, .mouseMoved, .activeInActiveApp],
            owner: self,
            userInfo: nil
        )
        addTrackingArea(trackingArea)
    }
    
    override func mouseEntered(with event: NSEvent) {
        print("Mouse entered the view")
    }
    
    override func mouseExited(with event: NSEvent) {
        print("Mouse exited the view")
    }
    
    override func mouseMoved(with event: NSEvent) {
        let mouseLocation = event.locationInWindow
        print("Mouse moved to: \(mouseLocation)")
    }
}
```

#### 4. **管理跟踪区域**

* **添加跟踪区域**: 使用 `addTrackingArea(_:)` 方法将 `NSTrackingArea` 添加到视图。
* **移除跟踪区域**: 使用 `removeTrackingArea(_:)` 方法可以从视图中移除特定的跟踪区域。

#### 5. **注意事项**

* 确保在视图的 `resetCursorRects()` 方法中调用 `super.resetCursorRects()`，以便更新光标状态。
* 跟踪区域的矩形可能会随视图的大小变化而改变，需要在视图大小变化时重新设置。

`NSTrackingArea` 是管理鼠标事件的强大工具，使用得当可以提升用户交互体验。
