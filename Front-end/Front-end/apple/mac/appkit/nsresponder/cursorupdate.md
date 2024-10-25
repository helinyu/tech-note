# cursorUpdate

`cursorUpdate(_:)` 方法用于处理光标的更新事件。<mark style="color:red;">当鼠标光标在视图或窗口内移动时，系统会调用此方法，以允许开发者根据光标的位置或状态更新光标的样式。</mark>

#### 调用时机

* **光标更新**: 当鼠标光标在视图内移动或更改状态时，`cursorUpdate(_:)` 方法被触发。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `cursorUpdate(_:)`：

```swift
import Cocoa

class CustomView: NSView {
    override func cursorUpdate(with event: NSEvent) {
        // 处理光标更新事件
        let mouseLocation = event.locationInWindow
        
        // 根据鼠标位置决定光标样式
        if mouseLocation.x < bounds.midX {
            NSCursor.pointingHand.set() // 左侧使用手形光标
        } else {
            NSCursor.arrow.set() // 右侧使用箭头光标
        }
    }
    
    override func acceptsFirstResponder() -> Bool {
        return true // 确保视图可以接收输入事件
    }
}
```

#### 说明

1. **`event` 参数**: `NSEvent` 对象包含有关光标更新的信息，可以使用 `event.locationInWindow` 获取鼠标在窗口中的位置。
2. **执行操作**: 在 `cursorUpdate(_:)` 方法中，可以根据鼠标位置或其他条件设置不同的光标样式，例如使用 `NSCursor` 的各种静态方法来改变光标。
3. **接受第一响应者**: 确保视图实现 `acceptsFirstResponder()` 方法并返回 `true`，以确保能够接收输入事件。

#### 注意事项

* 该方法通常在视图的每次更新过程中被调用，因此应考虑性能，避免在此方法中执行过于复杂的操作。
* 可以结合 `NSTrackingArea` 来更精确地控制光标样式的变化。

通过 `cursorUpdate(_:)` 方法，开发者可以灵活地根据用户的光标位置提供反馈，增强用户交互体验，使应用更加友好和直观。
