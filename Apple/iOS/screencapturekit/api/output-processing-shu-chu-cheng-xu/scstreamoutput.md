# SCStreamOutput

```
//  Receiving stream output 接收流的输出
@available(macOS 12.3, *)
public protocol SCStreamOutput : NSObjectProtocol {
    // 返回屏幕样本缓冲区的协议方法
    optional func stream(_ stream: SCStream, didOutputSampleBuffer sampleBuffer: CMSampleBuffer, of type: SCStreamOutputType)
}

```
