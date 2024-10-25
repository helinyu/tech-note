# isReleasedWhenClosed



{% hint style="info" %}
直接使用NSWindow 以及其子类，一定要设置这个，即为关闭不是放，设置为true，就会崩溃。 newWindow.isReleasedWhenClosed = false —— 建议使用NSwindowController来处理。
{% endhint %}



`isReleasedWhenClosed` 是 `NSWindow` 的一个属性，用于控制窗口在关闭时是否会被释放。如果将此属性设置为 `true`，那么当窗口关闭时，它将被自动释放；如果设置为 `false`，则窗口对象会保持在内存中，即使它已经关闭。这在某些情况下非常有用，例如当你希望重新显示窗口时，而不必重新创建它。

#### 使用示例

```swift
let newWindow = NSWindow(
    contentRect: NSRect(x: 0, y: 0, width: 540, height: 200),
    styleMask: [.titled, .closable, .resizable],
    backing: .buffered,
    defer: false
)

newWindow.isReleasedWhenClosed = false  // 设置为 false，保持在内存中
```

#### 何时使用

* **设置为 `true`**：
  * 如果窗口不再需要，且你希望释放内存。
* **设置为 `false`**：
  * 如果你可能会多次显示该窗口，或者希望保持窗口的状态和数据。

如果你的窗口在关闭时崩溃，可以考虑设置 `isReleasedWhenClosed` 为 `false`，并在适当的时机手动释放资源。





