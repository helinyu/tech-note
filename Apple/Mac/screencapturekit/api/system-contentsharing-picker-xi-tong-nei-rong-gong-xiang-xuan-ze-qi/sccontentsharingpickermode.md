# SCContentSharingPickerMode

```
//  选择器的模式
@available(macOS 14.0, *)
public struct SCContentSharingPickerMode : OptionSet, @unchecked Sendable {

    public init(rawValue: UInt)

    public static var singleWindow: SCContentSharingPickerMode { get } // 单窗口
    public static var multipleWindows: SCContentSharingPickerMode { get } // 多窗口
    public static var singleApplication: SCContentSharingPickerMode { get } // 单应用
    public static var multipleApplications: SCContentSharingPickerMode { get } // 多应用
    public static var singleDisplay: SCContentSharingPickerMode { get } // 单展示器
}

```
