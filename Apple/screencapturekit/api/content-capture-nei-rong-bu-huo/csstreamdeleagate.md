# CSStreamDeleagate

```
@available(macOS 12.3, *)
public protocol SCStreamDelegate : NSObjectProtocol {
    
// 《1》Responding to Presenter Overlay 回应显示着的叠加
    @available(macOS 14.0, *)
    optional func outputVideoEffectDidStart(for stream: SCStream)
    @available(macOS 14.0, *)
    optional func outputVideoEffectDidStop(for stream: SCStream)


// 《2》Responding to stream stoppage 响应流的故障
    optional func stream(_ stream: SCStream, didStopWithError error: any Error)

    //  《3》 Instance Methods 实例的方法，流是通过用户通过控制中心模块来停止的（即为认为停止的—— 正常停止状态）
    @available(macOS 14.4, *)
    optional func userDidStopStream(_ stream: SCStream)
}

```
