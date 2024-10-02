---
description: 流对象： 初始化、更新配置(contentfilter/config)、开始/结束
---

# SCStream\[流]

```
@available(macOS 12.3, *)
open class SCStream : NSObject {

    //   始终同步媒体捕获 —— 同步作用
    @available(macOS 13.0, *)
    open var synchronizationClock: CMClock? { get }

    
    //   初始化，创建一个stream对象
    //  contentFilter 内容过滤器
    //  streamConfig 流配置
    //  delegate 代理
    //  创建一个stream对象并且有指定的内容输出设置
    public init(filter contentFilter: SCContentFilter, configuration streamConfig: SCStreamConfiguration, delegate: (any SCStreamDelegate)?)

    //  给当前的session添加/删除 输出配置
    open func addStreamOutput(_ output: any SCStreamOutput, type: SCStreamOutputType, sampleHandlerQueue: dispatch_queue_t?) throws
    open func removeStreamOutput(_ output: any SCStreamOutput, type: SCStreamOutputType) throws

    
    //  更新shareablecontent的过滤器
    open func updateContentFilter(_ contentFilter: SCContentFilter, completionHandler: (((any Error)?) -> Void)? = nil)
    open func updateContentFilter(_ contentFilter: SCContentFilter) async throws

    
    //  更新配置
    // streamConfig 
    open func updateConfiguration(_ streamConfig: SCStreamConfiguration, completionHandler: (((any Error)?) -> Void)? = nil)
    open func updateConfiguration(_ streamConfig: SCStreamConfiguration) async throws

//  这两个都是更新： 
// updateContentFilter 针对的是shareContent
// updateConfiguration 针对大的是stream
    


    //  开始或者停止捕获
    open func startCapture(completionHandler: (((any Error)?) -> Void)? = nil)
    open func startCapture() async throws
    open func stopCapture(completionHandler: (((any Error)?) -> Void)? = nil)
    open func stopCapture() async throws
}

```





