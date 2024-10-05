# 8、WKWebView loadRequest 问题

WKWebView 通过loadrequest方法加载Post请求会丢失请求体（body）中的内容，进而导致服务器拿不到body中的内容的问题的发生。这个问题的产生主要是因为WKWebView的网络请求的进程与APP不是同一个进程，所以网络请求的过程是这样的：

由APP所在的进程发起request，然后通过IPC通信(进程间通信)将请求的相关信息（请求头、请求行、请求体等）传递给webkit网络线进程接收包装，进行数据的HTTP请求，最终再进行IPC的通信回传给APP所在的进程的。这里如果发起的request请求是post请求的话，由于要进行IPC数据传递，传递的请求体body中根据系统调度，将其舍弃，最终在WKWebView网络进程接受的时候请求体body中的内容变成了空，导致此种情况下的服务器获取不到请求体，导致问题的产生。

**解决问题：**

1.将网络请求交由Js发起，绕开系统WKWebView的网络的进程请求达到正常请求的目的

2.改变POST请求的方法为GET方法(有风险，不一定服务器会接受GET方法)

3.将Post请求的请求body内容放入请求的Header中，并通过URLProtocol拦截自定义协议，在拦截中通过NSConnection进行重新请求（重新包装请求body），然后通过回调Client客户端来传递数据内容

3，WKWebView 页面样式问题\
在 WKWebView 适配过程中，发现部分H5页面元素位置向下偏移或被拉伸变形，追踪后发现主要是H5页面高度值异常导致：\
解决方案：\
调整WKWebView布局方式，避免调整webView.scrollView.contentInset。实际上，即便在 UIWebView 上也不建议直接调整webView.scrollView.contentInset的值，这确实会带来一些奇怪的问题。如果某些特殊情况下非得调整 contentInset 不可的话，可以通过下面方式让H5页面恢复正常显示：

{% code overflow="wrap" %}
```
/**设置contentInset值后通过调整webView.frame让页面恢复正常显示 *参考：http://km.oa.com/articles/show/277372 */

webView.scrollView.contentInset = UIEdgeInsetsMake(a, 0, 0, 0); 

webView.frame = CGRectMake(webView.frame.origin.x, webView.frame.origin.y, webView.frame.size.width, webView.frame.size.height - a);
```
{% endcode %}

4，视频自动播放\
WKWebView 需要通过WKWebViewConfiguration.mediaPlaybackRequiresUserAction设置是否允许自动播放，但一定要在 WKWebView 初始化之前设置，在 WKWebView 初始化之后设置无效。
