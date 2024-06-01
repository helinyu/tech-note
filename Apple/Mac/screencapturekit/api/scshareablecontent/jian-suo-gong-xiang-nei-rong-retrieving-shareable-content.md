---
description: 检索共享内容
---

# \[检索共享内容]Retrieving shareable content

```
@available(macOS 12.3, *)
open class SCShareableContent : NSObject {


    //  返回SCShareableContent 对象，
    //  包括windows、displays、applications
    open class func getWithCompletionHandler(_ completionHandler: @escaping (SCShareableContent?, (any Error)?) -> Void)

    // 这个对象就是包括windows、displays、applications
    open class var current: SCShareableContent { get async throws }

    
    

//  配置
// excludeDesktopWindows 不包括桌面窗口
// onScreenWindowsOnly 只有屏幕窗口
    open class func getExcludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnly: Bool, completionHandler: @escaping (SCShareableContent?, (any Error)?) -> Void)
    open class func excludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnly: Bool) async throws -> SCShareableContent

// onScreenWindowsOnlyBelow 在屏幕窗口下面
    open class func getExcludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnlyBelow window: SCWindow, completionHandler: @escaping (SCShareableContent?, (any Error)?) -> Void)
    open class func excludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnlyBelow window: SCWindow) async throws -> SCShareableContent

// onScreenWindowsOnlyAbove 在屏幕窗口上面
    open class func getExcludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnlyAbove window: SCWindow, completionHandler: @escaping (SCShareableContent?, (any Error)?) -> Void)
    open class func excludingDesktopWindows(_ excludeDesktopWindows: Bool, onScreenWindowsOnlyAbove window: SCWindow) async throws -> SCShareableContent

    //  过滤的信息
    @available(macOS 14.0, *)
    open class func info(for filter: SCContentFilter) -> SCShareableContentInfo

    
//  窗口对象
    open var windows: [SCWindow] { get }

    
//  显示对象
    open var displays: [SCDisplay] { get }

    
// 应用程序对象
    open var applications: [SCRunningApplication] { get }
}

```

```
// 共享内容信息
@available(macOS 14.0, *)
open class SCShareableContentInfo : NSObject {

//  流的类型
    open var style: SCShareableContentStyle { get }

    
    // 像素点
    open var pointPixelScale: Float { get }
  
// 位置大小
    open var contentRect: CGRect { get }
}

//  共享内容样式
public enum SCShareableContentStyle : Int, @unchecked Sendable {

    case none = 0

    case window = 1 
    // 窗口，一个应用有多个窗口

    case display = 2 
    //显示设备（显示器），一台设备可能连接多个显示器

    case application = 3 
    // 应用程序
}
```
