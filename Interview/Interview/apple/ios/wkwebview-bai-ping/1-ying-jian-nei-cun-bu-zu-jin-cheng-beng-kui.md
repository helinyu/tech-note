# 1、硬件内存不足、进程崩溃

在 UIWebView 上当内存占用太大的时候，App Process 会 crash；

而在 WKWebView 上当总体的内存占用比较大的时候，WebContent Process 会 crash，从而出现白屏现象。



这个时候 WKWebView.URL 会变为 nil, 简单的 reload 刷新操作已经失效，对于一些长驻的H5页面影响比较大。

我们最后的解决方案是：

A、借助 WKNavigtionDelegate

iOS 9以后 WKNavigtionDelegate 新增了一个回调函数：

```
- (void)webViewWebContentProcessDidTerminate:(WKWebView *)webView API_AVAILABLE(macosx(10.11), ios(9.0));
```

当 WKWebView 总体内存占用过大，页面即将白屏的时候，系统会调用上面的回调函数，我们在该函数里执行\[webView reload]\(这个时候 webView.URL 取值尚不为 nil）解决白屏问题。在一些高内存消耗的页面可能会频繁刷新当前页面，H5侧也要做相应的适配操作。

B、检测 webView.title 是否为空 并不是所有H5页面白屏的时候都会调用上面的回调函数，比如，最近遇到在一个高内存消耗的H5页面上 present 系统相机，拍照完毕后返回原来页面的时候出现白屏现象（拍照过程消耗了大量内存，导致内存紧张，WebContent Process 被系统挂起），但上面的回调函数并没有被调用。在WKWebView白屏的时候，另一种现象是 webView.titile 会被置空, 因此，可以在 viewWillAppear 的时候检测 webView.title 是否为空来 reload 页面。
