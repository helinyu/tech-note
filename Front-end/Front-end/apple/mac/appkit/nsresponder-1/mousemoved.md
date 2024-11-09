# mouseMoved

`mouseMoved(with:)` 方法用于处理鼠标移动事件。当用户在应用程序的窗口内移动鼠标光标时，该方法被调用。它是 `NSResponder` 的一部分，通常在自定义视图或控制器中重写，以响应鼠标移动的交互。

#### 调用时机

* **鼠标移动**: 当用户在应用程序的窗口内移动鼠标时，如果视图是当前的第一响应者，`mouseMoved(with:)` 方法就会被触发。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `mouseMoved(with:)`：

```swift
import Cocoa

class CustomView: NSView {
    override func viewDidMoveToWindow() {
        super.viewDidMoveToWindow()
        
        let trackingArea = NSTrackingArea(rect: self.bounds,
                                           options: [.mouseMoved, .activeAlways],
                                           owner: self,
                                           userInfo: nil)
        self.addTrackingArea(trackingArea)
    }

    override func mouseMoved(with event: NSEvent) {
        // 处理鼠标移动事件
        let mouseLocation = event.locationInWindow
        print("Mouse moved to: \(mouseLocation)")
        
        // 可以在这里更新界面，例如显示鼠标位置或高亮某个元素
    }
}
```

#### 说明

1. **添加追踪区域**: 在 `viewDidMoveToWindow()` 方法中，使用 `NSTrackingArea` 添加一个追踪区域，以确保视图能够接收鼠标移动事件。`options` 参数可以包括 `.mouseMoved` 选项，表示该视图将响应鼠标移动事件。
2. **`mouseMoved(with:)`**: 当鼠标移动到该视图内时，该方法被调用。你可以使用 `event.locationInWindow` 获取鼠标在窗口中的当前位置，并执行相应的操作，例如更新 UI 或显示鼠标位置。

#### 注意事项

* 如果视图没有添加追踪区域，`mouseMoved(with:)` 方法将不会被调用。
* 在处理鼠标移动事件时，可以考虑性能，特别是在需要频繁更新 UI 的情况下，确保更新操作不会导致界面卡顿。

通过 `mouseMoved(with:)` 方法，开发者可以灵活地处理用户的鼠标移动操作，从而实现丰富的交互体验，例如实时显示信息或动态更新界面元素。
