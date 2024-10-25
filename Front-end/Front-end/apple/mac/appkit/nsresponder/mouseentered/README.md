# mouseEntered

`mouseEntered(_:)` 方法用于处理鼠标光标进入某个追踪区域的事件。当用户的鼠标光标进入由 `NSTrackingArea` 定义的区域时，该方法被调用。这通常用于实现鼠标悬停效果，比如高亮显示、显示提示信息或改变界面元素的状态。

#### 调用时机

* **鼠标进入追踪区域**: 当鼠标光标进入由 `NSTrackingArea` 定义的区域时，`mouseEntered(_:)` 方法被触发。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `mouseEntered(_:)`：

```swift
import Cocoa

class CustomView: NSView {
    override func viewDidMoveToWindow() {
        super.viewDidMoveToWindow()
        
        let trackingArea = NSTrackingArea(rect: self.bounds,
                                           options: [.mouseEnteredAndExited, .activeAlways],
                                           owner: self,
                                           userInfo: nil)
        self.addTrackingArea(trackingArea)
    }

    override func mouseEntered(with event: NSEvent) {
        // 处理鼠标进入事件
        print("Mouse entered the view!")
        self.layer?.backgroundColor = NSColor.yellow.cgColor // 示例：更改背景颜色
    }

    override func mouseExited(with event: NSEvent) {
        // 处理鼠标退出事件
        print("Mouse exited the view!")
        self.layer?.backgroundColor = NSColor.clear.cgColor // 示例：恢复背景颜色
    }
}
```

#### 说明

1. **添加追踪区域**: 在 `viewDidMoveToWindow()` 方法中，使用 `NSTrackingArea` 添加一个追踪区域，选择 `.mouseEnteredAndExited` 选项，以便同时响应鼠标进入和退出事件。
2. **`mouseEntered(with:)`**: 当鼠标光标进入追踪区域时，这个方法被调用。在这里，你可以执行任何需要的操作，例如更改视图的外观或更新界面状态。
3. **`mouseExited(with:)`**: 这个方法在鼠标离开追踪区域时被调用，可以在这里进行相应的清理操作，比如恢复视图的状态。

通过 `mouseEntered(_:)` 方法，开发者可以增强用户交互体验，提供动态反馈，例如高亮显示元素或显示额外的信息。
