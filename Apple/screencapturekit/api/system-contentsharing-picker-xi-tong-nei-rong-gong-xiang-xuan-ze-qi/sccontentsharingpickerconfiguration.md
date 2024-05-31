# SCContentSharingPickerConfiguration

```
//  picker的配置
@available(macOS 14.0, *)
public struct SCContentSharingPickerConfiguration {

    //  《1》初始化
    public init() 

    //  《2》Control streaming selections 控制流的选择
    public var allowedPickerModes: SCContentSharingPickerMode // 允许的模式

    public var excludedWindowIDs: [Int] // 排除掉的windowIDS

    public var excludedBundleIDs: [String] // 排除掉的bundleIDs

    public var allowsChangingSelectedContent: Bool // 允许改变选择内容
}
```
