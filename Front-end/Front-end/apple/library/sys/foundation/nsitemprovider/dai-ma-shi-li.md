# 代码示例

在 SwiftUI 环境中，我们可以使用 `NSItemProvider` 来处理拖放操作、复制粘贴等数据共享任务。下面是一个在 SwiftUI 中使用 `NSItemProvider` 处理文本、图片和 URL 数据的完整代码示例。

#### 完整代码示例

```swift
import SwiftUI

struct ContentView: View {
    @State private var loadedText: String = ""
    @State private var loadedImage: UIImage? = nil
    @State private var loadedURL: URL? = nil

    var body: some View {
        VStack {
            // 文本展示
            if !loadedText.isEmpty {
                Text("Loaded Text: \(loadedText)")
                    .padding()
            } else {
                Text("No text loaded")
                    .padding()
            }
            
            // 图片展示
            if let image = loadedImage {
                Image(uiImage: image)
                    .resizable()
                    .frame(width: 200, height: 200)
                    .padding()
            } else {
                Text("No image loaded")
                    .padding()
            }
            
            // URL 展示
            if let url = loadedURL {
                Text("Loaded URL: \(url.absoluteString)")
                    .padding()
            } else {
                Text("No URL loaded")
                    .padding()
            }
            
            Button("Load Data") {
                loadData()
            }
            .padding()
        }
    }

    // 加载数据的函数
    func loadData() {
        // 文本数据处理
        let textProvider = NSItemProvider(object: "This is a sample text" as NSString)
        if textProvider.canLoadObject(ofClass: NSString.self) {
            textProvider.loadObject(ofClass: NSString.self) { (object, error) in
                if let text = object as? String {
                    DispatchQueue.main.async {
                        self.loadedText = text
                    }
                }
            }
        }

        // 图片数据处理
        if let sampleImage = UIImage(systemName: "photo") {
            let imageProvider = NSItemProvider(object: sampleImage)
            if imageProvider.canLoadObject(ofClass: UIImage.self) {
                imageProvider.loadObject(ofClass: UIImage.self) { (object, error) in
                    if let image = object as? UIImage {
                        DispatchQueue.main.async {
                            self.loadedImage = image
                        }
                    }
                }
            }
        }

        // URL 数据处理
        if let sampleURL = URL(string: "https://www.example.com") {
            let urlProvider = NSItemProvider(object: sampleURL as NSURL)
            if urlProvider.canLoadObject(ofClass: NSURL.self) {
                urlProvider.loadObject(ofClass: NSURL.self) { (object, error) in
                    if let url = object as? URL {
                        DispatchQueue.main.async {
                            self.loadedURL = url
                        }
                    }
                }
            }
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

#### 代码解析

1. **`@State` 变量**：
   * `@State` 用于管理 SwiftUI 界面的状态，存储从 `NSItemProvider` 加载的数据，例如 `loadedText`（文本）、`loadedImage`（图片）和 `loadedURL`（URL）。
2. **`NSItemProvider` 的使用**：
   * 为文本、图片和 URL 数据分别创建了 `NSItemProvider` 实例。
   * 使用 `canLoadObject(ofClass:)` 方法检查是否支持加载特定类型的数据。
   * 通过 `loadObject(ofClass:completionHandler:)` 异步加载数据，并在数据加载完成后更新 `@State` 状态，从而更新 UI。
3. **界面布局**：
   * 使用 `VStack` 将加载的文本、图片和 URL 显示在界面上。
   * 使用 `Image(uiImage:)` 展示加载的图片。
   * 一个按钮触发 `loadData()` 函数，模拟数据加载。

#### 运行效果

* 按下 **Load Data** 按钮后，程序将尝试加载文本、图片和 URL 并显示在界面上。
* 文本、图片和 URL 分别使用 `NSItemProvider` 加载并异步处理，然后更新 SwiftUI 的界面。

这就是在 SwiftUI 环境下如何使用 `NSItemProvider` 的完整代码示例，适用于处理不同类型的数据并在界面上动态显示结果。
