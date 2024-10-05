# 4、 HTTPS 请求，未实现证书认证代理导致页面不加载的问题

如果是HTTPS 请求，需要在WKWebView 的 WKNavigationDelegate 中的一个代理方法 中实现获取服务器认证的逻辑，最后返回给服务端。

&#x20;这个问题常常出现在客户端无法获得安全认证的时候（没有证书，或者是自建证书），

比如说https://www.apple.com/cn 是默认的苹果中国的地址，但是 https://www.apple.com.cn 也是可以访问的（会自动跳转到 https://www.apple.com/cn ) ，只是在Safari 的安全认证中通不过，我们需要在代理方法中通过服务端给的验证方式创建一个凭证，然后继续申请访问。比如在Safari 浏览器中第一次访问时就会弹出对话框，点击继续后就可以继续访问。

{% code title="实现代理解决" overflow="wrap" %}
```
func webView(webView: WKWebView, didReceiveAuthenticationChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void)
{  // 判断服务器采用的验证方法
    if challenge.protectionSpace.authenticationMethod == NSURLAuthenticationMethodServerTrust {
        if challenge.previousFailureCount == 0 {
            // 如果没有错误的情况下 创建一个凭证，并使用证书
            let credential = NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!)
            completionHandler(.UseCredential, credential)
        } else {
            // 验证失败，取消本次验证
            completionHandler(.CancelAuthenticationChallenge, nil)
        }
    } else {
        completionHandler(.CancelAuthenticationChallenge, nil)
    }
}

```
{% endcode %}
