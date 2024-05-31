# SCContentFilter

```

// 是对shareContent的filter，从而影响捕获的流
@available(macOS 12.3, *)
open class SCContentFilter : NSObject {

//  《1》Creating a filter 创建一个过滤器 ，通过配置shareContent的内容创建
    public init(desktopIndependentWindow window: SCWindow)
    public init(display: SCDisplay, excludingWindows excluded: [SCWindow])
    public init(display: SCDisplay, including includedWindows: [SCWindow])
    public init(display: SCDisplay, including applications: [SCRunningApplication], exceptingWindows: [SCWindow])
    public init(display: SCDisplay, excludingApplications applications: [SCRunningApplication], exceptingWindows: [SCWindow])

// 《2》Filter properties 过滤器的属性
    open var pointPixelScale: Float { get } // 带你像素因子
    open var contentRect: CGRect { get } // 内容的位置大小
    @available(macOS, introduced: 14.0, deprecated: 14.2, message: "Use style instead")
    open var streamType: SCStreamType { get } // 流的类型
    //  流类型
    public enum SCStreamType : Int, @unchecked Sendable {
        case window = 0
        case display = 1
    }

    open var style: SCShareableContentStyle { get } //共享内容的样式

//  《3》Instance Properties 实例属性
//  包括菜单栏是否捕获。 这个属性对桌面独立的过滤器不影响
//  对于使用initWithDisplay:excluding 方法创建的，默认是YES。 display的excluding包括desktop和dock
//  对于使用initWithDisplay:including 方法创建的，默认是NO，display的including不包括desktop和dock
    @available(macOS 14.2, *)
    open var includeMenuBar: Bool
}
```
