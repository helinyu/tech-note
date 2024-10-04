# UIWebView

`UIWebView` 是 iOS 中最早用于在应用程序内嵌显示网页内容的组件，在 iOS 2.0 中首次引入。尽管 `UIWebView` 功能强大，但其设计相对较旧，性能和灵活性不如其后继者 `WKWebView`。自 iOS 8.0 推出 `WKWebView` 以来，`UIWebView` 已被逐渐废弃，并最终在 iOS 12.0 后被完全弃用。

#### 1. **基本功能**

* **网页渲染**\
  `UIWebView` 可以加载和显示 HTML 页面，包括本地文件和远程 URL，支持基本的 HTML、CSS、JavaScript 渲染。
* **JavaScript 支持**\
  `UIWebView` 可以执行网页中的 JavaScript，但它的 JavaScript 处理速度较慢，且与应用的交互相对复杂。相比之下，`WKWebView` 提供了更高效和现代化的 JavaScript 交互机制。
* **导航功能**\
  `UIWebView` 支持基本的网页导航操作，如前进、后退和刷新等功能。不过，这些操作的性能较低，尤其是在加载大文件或复杂网页时。

#### 2. **加载网页内容的方式**

`UIWebView` 提供了多种加载网页内容的方法：

*   **加载 URL**\
    通过 `loadRequest(_:)` 方法可以加载远程网页或本地资源。例如：

    ```swift
    let webView = UIWebView(frame: .zero)
    let url = URL(string: "https://www.apple.com")!
    let request = URLRequest(url: url)
    webView.loadRequest(request)
    ```
*   **加载 HTML 字符串**\
    你可以通过 `loadHTMLString(_:baseURL:)` 方法直接加载 HTML 字符串：

    ```swift
    let htmlString = "<html><body><h1>Hello, World!</h1></body></html>"
    webView.loadHTMLString(htmlString, baseURL: nil)
    ```
*   **加载本地文件**\
    使用本地文件路径加载 HTML 文件也十分方便：

    ```swift
    if let filePath = Bundle.main.path(forResource: "index", ofType: "html") {
        let url = URL(fileURLWithPath: filePath)
        let request = URLRequest(url: url)
        webView.loadRequest(request)
    }
    ```

#### 3. **委托协议**

*   **`UIWebViewDelegate`**\
    `UIWebView` 依赖于 `UIWebViewDelegate` 来处理页面的加载事件。常见的委托方法包括：

    * `webViewDidStartLoad(_:)`：网页开始加载时调用。
    * `webViewDidFinishLoad(_:)`：网页加载完成时调用。
    * `webView(_:didFailLoadWithError:)`：加载失败时调用。

    相比于 `WKWebView` 的 `WKNavigationDelegate`，`UIWebView` 的代理机制较为简单，功能也较为有限。

#### 4. **性能问题**

* **单进程架构**\
  <mark style="color:red;">**`UIWebView`**</mark><mark style="color:red;">** **</mark><mark style="color:red;">**是单进程架构，网页内容与应用程序运行在同一个进程中**</mark>。这意味着，如果网页内容过于复杂，导致渲染崩溃，整个应用也可能崩溃。此外，JavaScript 的执行性能也受到单进程架构的限制，性能较为低下。
* **内存消耗高**\
  `UIWebView` 的内存管理较为糟糕，加载复杂网页时容易导致内存泄漏，尤其在 iOS 设备的内存较为有限时容易导致应用崩溃。
* **响应慢**\
  尤其在处理大量 JavaScript 或渲染复杂网页时，`UIWebView` 的响应速度明显较慢，用户体验不佳。`WKWebView` 在这方面有显著改进。

#### 5. **JavaScript 执行**

`UIWebView` 支持通过 `stringByEvaluatingJavaScript(from:)` 执行 JavaScript 代码，但该方法是<mark style="color:red;">**同步**</mark><mark style="color:red;">的，容易阻塞主线程</mark>，<mark style="color:red;">且无法获取执行结果中的错误信息</mark>。例如：

```swift
let result = webView.stringByEvaluatingJavaScript(from: "document.title")
print("Page title: \(result ?? "")")
```

与之相比，`WKWebView` 提供了更为先进的异步方法 `evaluateJavaScript(_:completionHandler:)`，避免了主线程阻塞。

#### 6. **用户体验和局限性**

* **无进程隔离**\
  由于 `UIWebView` 采用单进程架构，没有与应用程序隔离的网页内容渲染子进程，网页崩溃时会导致整个应用崩溃，影响用户体验。
* **缺少现代化特性**\
  `UIWebView` 不支持许多现代化的网页特性和协议，像 HTML5 视频播放、WebGL 渲染、离屏渲染等功能在 `UIWebView` 中的支持都有限或缺失。
* **缺少缓存和 Cookie 管理**\
  `UIWebView` 的缓存和 Cookie 管理相对简单且不灵活，没有像 `WKWebView` 那样的高级 API 可以灵活地管理网页存储数据。

#### 7. **弃用**

苹果在 iOS 8 推出了更先进的 `WKWebView`，并在之后逐渐弃用了 `UIWebView`。在 iOS 12 及更高版本中，`UIWebView` 不再被推荐使用，开发者被强烈建议迁移到 `WKWebView`。

#### 总结

`UIWebView` 曾是 iOS 中显示网页内容的主要工具，但由于其性能、稳定性和安全性方面的局限性，它已被淘汰。相比之下，`WKWebView` 提供了更现代的特性，包括更高效的多进程架构、更好的内存管理以及更强大的 JavaScript 交互能力。因此，开发者应避免使用 `UIWebView`，并迁移到 `WKWebView`。
