---
description: 用来开发截图工具的好方法
---

# SCScreenshotmanger

```

@available(macOS 14.0, *)
open class SCScreenshotManager : NSObject {

// Individual frame capture 独立帧捕获
    
    //  返回CMSampleBuffer对象，通过使用filter和configuration
    @available(macOS 14.0, *)
    open class func captureSampleBuffer(contentFilter: SCContentFilter, configuration config: SCStreamConfiguration, completionHandler: ((CMSampleBuffer?, (any Error)?) -> Void)? = nil)
    @available(macOS 14.0, *)
    open class func captureSampleBuffer(contentFilter: SCContentFilter, configuration config: SCStreamConfiguration) async throws -> CMSampleBuffer

    // 返回一个CGImage对象，是RGBA的格式
    @available(macOS 14.0, *)
    open class func captureImage(contentFilter: SCContentFilter, configuration config: SCStreamConfiguration, completionHandler: ((CGImage?, (any Error)?) -> Void)? = nil)
    @available(macOS 14.0, *)
    open class func captureImage(contentFilter: SCContentFilter, configuration config: SCStreamConfiguration) async throws -> CGImage
}

```
