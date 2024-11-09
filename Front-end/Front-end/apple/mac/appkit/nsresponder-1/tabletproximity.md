# tabletProximity

`tabletProximity(with:)` 方法用于处理来自绘图板或触控设备的接近事件。当绘图工具（如数字笔或触控笔）接近绘图板时，该方法被调用。这对于绘图应用特别重要，因为它可以用于检测工具的存在并更新界面或状态。

#### 调用时机

* **接近事件**: 当数字笔或其他输入工具接近绘图板但尚未接触时，`tabletProximity(with:)` 方法被触发。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `tabletProximity(with:)`：

```swift
import Cocoa

class DrawingView: NSView {
    override func tabletProximity(with event: NSEvent) {
        // 处理绘图工具接近事件
        let isInProximity = event.isInProximity // 检查工具是否在接近范围内
        let pressure = event.pressure // 获取压力值（如果已接触）
        
        if isInProximity {
            print("Tablet tool is nearby.")
            // 可以在这里更新界面，例如显示工具提示或改变状态
        } else {
            print("Tablet tool is out of proximity.")
            // 可以在这里恢复界面状态或清理信息
        }
        
        // 如果工具已接触，可以使用 pressure 值进行进一步处理
    }
    
    override func acceptsFirstResponder() -> Bool {
        return true // 确保视图可以接收输入事件
    }
}
```

#### 说明

1. **`event` 参数**: `NSEvent` 对象包含关于接近事件的信息。可以使用 `event.isInProximity` 检查输入工具是否在接近范围内，还可以通过 `event.pressure` 获取压力值（如果工具已经接触）。
2. **执行操作**: 在这个方法中，你可以根据接近状态更新用户界面，例如显示工具提示、切换状态或调整绘图设置。
3. **接受第一响应者**: 确保视图实现 `acceptsFirstResponder()` 方法并返回 `true`，以使其能够接收输入事件。

#### 注意事项

* 这个方法特别适用于需要与绘图工具交互的应用，能够提供更流畅的用户体验。
* 根据不同的设备和工具，可能会有不同的接近事件特性，因此可以根据具体的硬件进行调整和优化。

通过 `tabletProximity(with:)` 方法，开发者可以检测绘图工具的接近状态，从而增强用户交互体验，特别是在绘图和创意应用中。
