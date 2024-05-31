# SCContentSharingPickerObserver

```
//  用来通知客户端，当picker做选择或者取消的时候，观察期
@available(macOS 14.0, *)
public protocol SCContentSharingPickerObserver : NSObjectProtocol {

//  《1》Observing events 监听事件
    func contentSharingPicker(_ picker: SCContentSharingPicker, didCancelFor stream: SCStream?)
    func contentSharingPicker(_ picker: SCContentSharingPicker, didUpdateWith filter: SCContentFilter, for stream: SCStream?)

    // 《2》Observing errors 观察期错误
    func contentSharingPickerStartDidFailWithError(_ error: any Error)
}
```
