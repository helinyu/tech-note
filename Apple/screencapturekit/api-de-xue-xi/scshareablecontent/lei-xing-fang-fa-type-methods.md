---
description: 类型方法 —— 一般的检索共享内容额方法
---

# \[类型方法]Type Methods

&#x20;// TCC概念：https://www.ithome.com.tw/news/148844

```

    //  和上上面方法类似，行的版本
    // 多了：这些信息可在未经用户同意的情况下通过TCC由当前流程捕获
    @available(macOS 14.4, *)
    open class func getCurrentProcessShareableContent(completionHandler: @escaping (SCShareableContent?, (any Error)?) -> Void)


    //  比较什么的current多了TCC这玩意
    @available(macOS 14.4, *)
    open class var currentProcess: SCShareableContent { get async throws }

```
