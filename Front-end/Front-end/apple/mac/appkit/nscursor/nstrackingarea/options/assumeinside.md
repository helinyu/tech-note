# assumeInside

`assumeInside` 是 `NSTrackingArea` 中的一个选项，它用于指示该跟踪区域在创建时假设鼠标在区域内。这对于初始化时希望立即处理鼠标事件的情况非常有用。

#### 使用场景

当你创建一个 `NSTrackingArea` 实例并希望假设鼠标当前位于该区域内时，可以使用 `assumeInside` 选项。例如，这在你希望在视图显示时立即更新界面或状态时特别有用。

#### 示例代码

以下是一个示例，展示如何使用 `assumeInside` 选项：

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
            options: [.mouseEntered, .mouseExited, .mouseMoved, .activeInActiveApp, .assumeInside],
            owner: self,
            userInfo: nil
        )
        addTrackingArea(trackingArea)
        
        // 假设鼠标当前在该区域内
        mouseEntered(with: NSEvent())
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

#### 说明

* **`assumeInside` 的效果**: 使用此选项后，`mouseEntered` 方法将在跟踪区域创建时立即被调用，允许你在视图首次显示时处理鼠标进入的事件，而不必等到鼠标实际进入该区域。
* **用途**: 这在需要立即更新 UI 状态或进行初始化时特别有用，比如改变光标、显示工具提示或更新视图的外观。

`assumeInside` 选项使得处理鼠标事件的逻辑更加灵活和便捷。
