# cursorUpdate

`cursorUpdate` 是 `NSResponder` 中的一个方法，用于在鼠标移动时更新光标的样式。这个方法在鼠标在视图中移动时会被调用，可以根据当前的鼠标位置和视图状态动态更新光标。

#### 使用场景

* 你可能希望根据鼠标的位置或视图的状态改变光标样式。例如，当鼠标悬停在某个可交互区域（如按钮或链接）时，可以显示手形光标；当鼠标悬停在其他区域时，可能希望显示箭头光标。

#### 方法签名

```swift
override func cursorUpdate(with event: NSEvent) {
    // 在这里更新光标样式
}
```

#### 示例代码

以下是一个示例，展示如何重写 `cursorUpdate(with:)` 方法以根据鼠标位置动态更新光标：

```swift
import Cocoa

class CustomView: NSView {
    override func cursorUpdate(with event: NSEvent) {
        let mouseLocation = event.locationInWindow
        
        // 检查鼠标位置并更新光标样式
        if bounds.contains(mouseLocation) {
            // 在视图内部，设置手形光标
            NSCursor.pointingHand.set()
        } else {
            // 在视图外部，设置箭头光标
            NSCursor.arrow.set()
        }
        
        // 触发光标更新事件
        super.cursorUpdate(with: event)
    }
}
```

#### 说明

* **动态更新光标**: 通过重写 `cursorUpdate(with:)` 方法，你可以在鼠标移动时动态更新光标样式，以提高用户体验。
* **与鼠标事件结合**: `cursorUpdate` 通常与其他鼠标事件（如 `mouseMoved`、`mouseEntered`、`mouseExited`）结合使用，以确保光标在不同状态下正确显示。

通过实现 `cursorUpdate(with:)` 方法，你可以实现灵活的光标样式变化，以增强用户界面的交互性。
