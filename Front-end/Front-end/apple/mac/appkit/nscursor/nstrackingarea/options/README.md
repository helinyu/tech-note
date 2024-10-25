# Options

```
  public struct Options : OptionSet, @unchecked Sendable {

        public init(rawValue: UInt)

        public static var mouseEnteredAndExited: NSTrackingArea.Options { get }

        public static var mouseMoved: NSTrackingArea.Options { get }

        public static var cursorUpdate: NSTrackingArea.Options { get }
              //根据当前的鼠标位置和视图状态动态更新光标。

        public static var activeWhenFirstResponder: NSTrackingArea.Options { get }

        public static var activeInKeyWindow: NSTrackingArea.Options { get }

        public static var activeInActiveApp: NSTrackingArea.Options { get }

        public static var activeAlways: NSTrackingArea.Options { get }

        public static var assumeInside: NSTrackingArea.Options { get }
用于指示该跟踪区域在创建时假设鼠标在区域内。这对于初始化时希望立即处理鼠标事件的情况非常有用。

        public static var inVisibleRect: NSTrackingArea.Options { get }
        在可见的范围内

        public static var enabledDuringMouseDrag: NSTrackingArea.Options { get }
        在鼠标拖动时保持跟踪区域的活动状态。

    }
```
