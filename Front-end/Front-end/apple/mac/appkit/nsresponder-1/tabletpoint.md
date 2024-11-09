# tabletPoint

`tabletPoint(with:)` 方法用于<mark style="color:red;">处理来自绘图板或触控板的输入事件。这些输入设备可以提供额外的信息，如压力、倾斜角度和其他感应数据，通常用于绘图应用或需要精确输入的场景。</mark>

#### 调用时机

* **绘图设备输入**: 当用户在绘图板上或触控板上进行触控时，`tabletPoint(with:)` 方法被调用。

#### 示例代码

以下是一个简单的示例，演示如何在自定义视图中使用 `tabletPoint(with:)`：

```swift
import Cocoa

class DrawingView: NSView {
    override func tabletPoint(with event: NSEvent) {
        // 处理来自绘图板的输入事件
        let point = event.locationInWindow
        let pressure = event.pressure // 获取压力值
        let tilt = event.tilt // 获取倾斜角度

        print("Tablet point at: \(point), Pressure: \(pressure), Tilt: \(tilt)")
        
        // 可以在这里执行绘图操作或其他基于输入的逻辑
    }
    
    override func acceptsFirstResponder() -> Bool {
        return true // 确保视图可以接收输入事件
    }
}
```

#### 说明

1. **`event` 参数**: `NSEvent` 对象包含关于绘图设备输入的信息。可以使用 `event.locationInWindow` 获取触控点的位置，使用 `event.pressure` 获取压力值，以及其他可用的感应信息（如倾斜角度等）。
2. **执行操作**: 在这个方法中，你可以根据触控板或绘图板的输入执行绘图或其他操作。
3. **接受第一响应者**: 确保视图实现 `acceptsFirstResponder()` 方法并返回 `true`，以使其能够接收输入事件。

#### 注意事项

* `tabletPoint(with:)` 方法特别适用于需要精确控制的应用，例如数字绘画、图形设计或其他创意应用。
* 根据设备的不同，可能会有不同的输入信息可用，因此可以根据具体的设备和需求进行扩展和处理。

通过 `tabletPoint(with:)` 方法，开发者可以充分利用绘图板或触控板的输入特性，提供丰富的用户交互体验，尤其在艺术和设计应用中。
