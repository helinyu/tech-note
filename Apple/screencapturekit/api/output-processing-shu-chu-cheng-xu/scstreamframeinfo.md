# SCStreamFrameInfo

```
// SCStreamFrameInfo 流帧率信息

// Default implementations 默认的实现
@available(macOS 12.3, *)
public struct SCStreamFrameInfo : Hashable, Equatable, RawRepresentable, @unchecked Sendable {

    public init(rawValue: String)
}
extension SCStreamFrameInfo {

//  SCStreamFrameInfo名字
// 《1》 Frame information constants 帧率信息常量
    @available(macOS 12.3, *)
    public static let status: SCStreamFrameInfo // SCStreamFrameInfoStatus

    @available(macOS 12.3, *)
    public static let displayTime: SCStreamFrameInfo // SCStreamFrameInfoDisplayTime 延迟时间

    @available(macOS 12.3, *)
    public static let scaleFactor: SCStreamFrameInfo // SCStreamFrameInfoScaleFactor scale因素 【1-4】

    @available(macOS 12.3, *)
    public static let contentScale: SCStreamFrameInfo // SCStreamFrameInfoContentScale 内容scale

    @available(macOS 12.3, *)
    public static let contentRect: SCStreamFrameInfo // SCStreamFrameInfoContentRect 内容位置和大小

    @available(macOS 12.3, *)
    public static let dirtyRects: SCStreamFrameInfo // key是 SCStreamFrameInfoDirtyRects

    @available(macOS 13.1, *)
    public static let screenRect: SCStreamFrameInfo // SCStreamFrameInfoScreenRect

    @available(macOS 14.0, *)
    public static let boundingRect: SCStreamFrameInfo // SCStreamFrameInfoBoundingRect

// Type Properties 类型属性
    @available(macOS 14.2, *)
    public static let presenterOverlayContentRect: SCStreamFrameInfo // SCStreamFrameInfoPresenterOverlayContentRect
}
```
