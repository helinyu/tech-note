# inVisibleRect

`inVisibleRect` 是 `NSTrackingArea` 的一个选项，主要用于跟踪可见区域内的鼠标事件。这个选项可以确保只有在视图的可见部分内触发鼠标事件，而忽略任何在不可见区域的鼠标移动。

#### 使用场景

* 当视图部分不可见（例如被遮挡或裁剪）时，你可能希望忽略那些不可见部分的鼠标事件。使用 `inVisibleRect` 可以避免处理无效的鼠标事件，从而提高性能和用户体验。

#### 示例代码

以下是一个使用 `inVisibleRect` 的示例，展示如何设置跟踪区域以仅在可见区域内响应鼠标事件：

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
            options: [.mouseEntered, .mouseExited, .mouseMoved, .inVisibleRect],
            owner: self,
            userInfo: nil
        )
        addTrackingArea(trackingArea)
    }
    
    override func mouseEntered(with event: NSEvent) {
        print("Mouse entered the visible part of the view")
    }
    
    override func mouseExited(with event: NSEvent) {
        print("Mouse exited the visible part of the view")
    }
    
    override func mouseMoved(with event: NSEvent) {
        let mouseLocation = event.locationInWindow
        print("Mouse moved to: \(mouseLocation)")
    }
}
```

#### 说明

* **`inVisibleRect` 的效果**: 通过这个选项，只有当鼠标在视图的可见区域内时，才会触发 `mouseEntered`、`mouseExited` 和 `mouseMoved` 方法。
* **优化性能**: 避免处理不可见区域的鼠标事件，可以减少不必要的处理，提高应用的性能。

使用 `inVisibleRect` 选项能够让你的视图在处理鼠标事件时更加高效和智能。
