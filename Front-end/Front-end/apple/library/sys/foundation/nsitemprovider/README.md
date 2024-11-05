# NSItemProvider

`NSItemProvider` 是 iOS 和 macOS 中用于在<mark style="color:red;">应用之间或应用内部共享数据的类</mark>，特别适用于处理剪贴板、拖放操作和文件共享。它抽象化了内容的提供和获取，可以处理多种不同类型的数据，例如文本、图像、文件等。

#### 主要功能

1. **跨应用数据传递**：通过拖放、复制粘贴等方式，可以在不同应用间传递数据。例如，用户可以将一个图片从图库拖到邮件应用中，`NSItemProvider` 会自动管理数据传递和类型转换。
2. **支持多种数据类型**：`NSItemProvider` 支持常见的数据类型，如文本、图像、文件、URL 等。你可以通过它处理来自多个源的不同数据类型。
3. **异步数据加载**：它支持异步加载数据，特别适合处理大文件或通过网络加载的资源。可以通过回调机制获取数据，避免阻塞主线程。

#### 常见用法

* **拖放操作**：在 iOS 11 及以上，`NSItemProvider` 常用于实现拖放功能。比如拖动图片到其他应用，数据通过 `NSItemProvider` 传递。
* **剪贴板**：`UIPasteboard` 类常用来实现复制粘贴功能，`NSItemProvider` 可以作为数据的容器。
* **共享扩展**：在共享扩展中使用 `NSItemProvider` 来传递不同类型的共享内容，比如通过社交媒体分享文本或图片。

#### 基本代码示例

以下是一个简单的示例，展示如何使用 `NSItemProvider` 处理文本数据：

```objc
NSItemProvider *provider = [[NSItemProvider alloc] initWithObject:@"This is a sample text"];
if ([provider canLoadObjectOfClass:[NSString class]]) {
    [provider loadObjectOfClass:[NSString class] completionHandler:^(NSString *string, NSError *error) {
        if (error == nil) {
            NSLog(@"Loaded string: %@", string);
        } else {
            NSLog(@"Error loading string: %@", error.localizedDescription);
        }
    }];
}
```

这个示例展示了如何使用 `NSItemProvider` 来处理异步加载文本数据。类似的，你也可以处理其他类型的数据，如 `UIImage`、`NSURL` 或自定义的数据类型。
