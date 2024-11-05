# 统预定义的环境键

SwiftUI 提供了一些系统预定义的环境键，允许你访问不同的环境值。以下是一些常用的环境键：

1. **`\.colorScheme`**：获取当前的颜色方案（`.light` 或 `.dark`）。
2. **`\.font`**：获取当前的默认字体。
3. **`\.locale`**：获取当前的区域设置。
4. **`\.sizeCategory`**：获取当前的文本大小类别（如 `.extraSmall`, `.large` 等）。
5. **`\.presentationMode`**：获取视图的呈现模式，通常用于管理视图的显示状态。
6. **`\.horizontalSizeClass`** 和 **`\.verticalSizeClass`**：获取当前的横向和纵向尺寸类别（如 `.compact` 或 `.regular`）。

#### 使用示例：

```swift
struct ContentView: View {
    @Environment(\.colorScheme) var colorScheme
    @Environment(\.font) var font

    var body: some View {
        VStack {
            Text("Current Color Scheme: \(colorScheme == .dark ? "Dark" : "Light")")
                .font(font) // 使用当前字体
        }
        .padding()
    }
}
```

#### 如何查找更多环境键：

* **文档**：查阅 Apple 的官方文档，了解可用的环境键及其使用方式。
* **源码**：你也可以查看 SwiftUI 的源代码，了解所有环境值和对应的键。

环境键为应用提供了灵活性，使得视图可以根据不同的上下文和系统设置自动调整其外观和行为。
