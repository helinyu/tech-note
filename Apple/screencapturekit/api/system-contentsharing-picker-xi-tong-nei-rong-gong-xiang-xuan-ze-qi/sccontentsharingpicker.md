# SCContentSharingPicker

```

// picker被创建用来控制中心选择的
@available(macOS 14.0, *)
open class SCContentSharingPicker : NSObject {

    //  《1》 Shared system picker 单例对象
    open class var shared: SCContentSharingPicker { get }

    // 《2》 Picker availability
    // 一个paicker需要标识为YES，才会显示出来。
    // 如果startPickingContent已经被调用，但是没有设置为YES，picker将不会显示
    open var isActive: Bool

    // 《4》Manage observers 管理监听者
    open func add(_ observer: any SCContentSharingPickerObserver) // 添加
    open func remove(_ observer: any SCContentSharingPickerObserver) // 删除

    
    //  《5》Picker display 显示
    open func present()
    open func present(using contentStyle: SCShareableContentStyle)
    open func present(for stream: SCStream)
    open func present(for stream: SCStream, using contentStyle: SCShareableContentStyle)
}

//  《3》Stream configuration 流的配置

@available(macOS 14.0, *)
extension SCContentSharingPicker {

    public var configuration: SCContentSharingPickerConfiguration?
    public var defaultConfiguration: SCContentSharingPickerConfiguration

    public var maximumStreamCount: Int? //最大流的数量

    public func setConfiguration(_ configuration: SCContentSharingPickerConfiguration?, for stream: SCStream)
}

```
