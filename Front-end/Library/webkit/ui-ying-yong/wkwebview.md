# WKWebview

`WKWebView` 是 iOS 和 macOS 上的一种用于嵌入网页内容的视图组件，属于 WebKit 框架的一部分。相比于其前身 `UIWebView`，`WKWebView` 提供了更高的性能和更先进的功能，特别是采用了多进程架构。

以下是关于 `WKWebView` 的主要内容和功能介绍：

#### 1. **基本功能**

* **网页渲染**\
  `WKWebView` 可以加载和展示 HTML、CSS、JavaScript 等网页内容，无论是本地的 HTML 文件还是远程的 URL。它支持现代 Web 标准，如 HTML5、CSS3 和 ECMAScript。
* **JavaScript 交互**\
  `WKWebView` 支持通过 `WKScriptMessageHandler` 与 JavaScript 进行双向通信。你可以在 JavaScript 中通过 `window.webkit.messageHandlers` 调用 Swift/Objective-C 方法，反之，Swift/Objective-C 代码也可以通过 `evaluateJavaScript` 方法执行 JavaScript 代码。
* **导航功能**\
  它支持各种导航功能，如前进、后退、刷新以及 URL 跳转，同时可以通过 `WKNavigationDelegate` 来管理这些导航事件。例如，可以捕捉是否允许跳转到某个 URL，或者监控页面加载的进度。

#### 2. **多进程架构**

正如前面提到的，`WKWebView` 使用多进程架构。网页内容是在一个独立的子进程中渲染的，而主应用程序运行在主进程中。这种设计能够提升安全性和稳定性，防止网页内容崩溃影响整个应用。

#### 3. **加载网页内容的方式**

`WKWebView` 支持多种加载网页内容的方式：

*   **加载 URL**\
    通过 `load(URLRequest)` 方法可以加载远程网页。例如：

    ```swift
    let webView = WKWebView(frame: .zero)
    let url = URL(string: "https://www.apple.com")!
    let request = URLRequest(url: url)
    webView.load(request)
    ```
*   **加载 HTML 字符串**\
    你可以通过 `loadHTMLString(_:baseURL:)` 方法加载本地 HTML 字符串：

    ```swift
    let htmlString = "<html><body><h1>Hello, World!</h1></body></html>"
    webView.loadHTMLString(htmlString, baseURL: nil)
    ```
*   **加载本地文件**\
    通过文件的 URL，你可以加载应用内的本地 HTML 文件：

    ```swift
    if let filePath = Bundle.main.path(forResource: "index", ofType: "html") {
        let url = URL(fileURLWithPath: filePath)
        webView.loadFileURL(url, allowingReadAccessTo: url)
    }
    ```

#### 4. **委托协议**

* **`WKNavigationDelegate`**\
  用于监控页面的加载过程。你可以实现它的以下方法来处理导航事件：
  * `webView(_:didStartProvisionalNavigation:)`：开始加载时调用。
  * `webView(_:didFinish:)`：网页加载完成时调用。
  * `webView(_:didFailProvisionalNavigation:withError:)`：加载失败时调用。
* **`WKUIDelegate`**\
  用于处理页面的 UI 相关内容，例如 JavaScript 警告框、确认框和输入框。

#### 5. **缓存与 Cookies 管理**

`WKWebView` 提供了丰富的缓存管理和 cookie 处理机制，可以通过 `WKWebsiteDataStore` 管理 cookie、缓存、数据库等数据。你可以获取所有网站的数据存储，也可以清除特定网站的缓存。

#### 6. **JavaScript 执行**

通过 `evaluateJavaScript(_:completionHandler:)`，你可以在 `WKWebView` 中执行 JavaScript 代码，并在完成后处理结果。例如：

```swift
webView.evaluateJavaScript("document.title") { (result, error) in
    if let title = result as? String {
        print("Page title: \(title)")
    }
}
```

#### 7. **性能优化**

* **离屏渲染**：`WKWebView` 可以支持离屏渲染，以提升复杂网页的渲染性能。
* **减少内存消耗**：相比于 `UIWebView`，`WKWebView` 显著减少了内存占用，尤其是在加载大型网页或包含大量图片的网页时。

#### 8. **支持的 API 和功能**

* **自定义用户代理**：通过 `customUserAgent` 属性可以设置自定义的用户代理字符串。
* **页面缩放**：支持通过 `allowsBackForwardNavigationGestures` 允许用户使用手势导航前进和后退。
* **内容策略**：通过 `contentMode` 属性来决定是否以移动设备模式或者桌面模式加载网页。

#### 9. **内存与持久化管理**

你可以通过 `WKWebsiteDataStore` 来管理 `WKWebView` 的持久化数据，比如缓存、Cookies、LocalStorage 等，也可以根据需求清理这些数据，提升应用性能。

#### 总结

`WKWebView` 是一个强大且高性能的网页视图组件，它支持现代 Web 标准并通过多进程架构确保安全性和稳定性。它提供了多种加载网页内容的方式、与 JavaScript 交互的能力，并且通过委托协议让开发者可以控制加载过程中的细节。
