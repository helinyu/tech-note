# mouseUp

和mousedown对应

`mouseUp(_:)` 方法用于处理鼠标按钮释放事件。当用户松开鼠标按钮时（通常是左键），这个方法会被调用。它是 `NSResponder` 的一部分，通常在自定义视图或控制器中重写，以实现特定的交互行为。

#### 调用时机

* **鼠标释放**: 当用户在应用程序的窗口内松开鼠标按钮时，`mouseUp(_:)` 方法被触发。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `mouseUp(_:)`：

```swift
import Cocoa

class CustomView: NSView {
    override func mouseUp(with event: NSEvent) {
        // 处理鼠标释放事件
        let mouseLocation = event.locationInWindow
        print("Mouse up at: \(mouseLocation)")
        
        // 可以在这里执行其他操作，比如结束拖动或确认选择
    }
}
```

#### 说明

1. **`event` 参数**: `NSEvent` 对象包含关于鼠标事件的信息，例如鼠标的当前位置、按下的按钮等。可以使用 `event.locationInWindow` 获取鼠标在窗口中的位置。
2. **执行操作**: 在这个方法中，你可以实现任意自定义的行为，例如结束拖动操作、确认选择或执行命令。

#### 注意事项

* 通常，`mouseDown(_:)` 和 `mouseUp(_:)` 方法会配合使用，以实现完整的鼠标点击交互。
* 如果需要处理鼠标的右键释放或其他按钮，可以重写 `rightMouseUp(_:)` 或 `otherMouseUp(_:)` 方法。

通过 `mouseUp(_:)` 方法，开发者可以灵活地处理用户的鼠标释放操作，从而实现丰富的交互体验。
