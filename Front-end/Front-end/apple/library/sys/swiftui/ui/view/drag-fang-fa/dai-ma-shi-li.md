# 代码示例

下面是一个简单的示例代码，演示如何使用 `onDrag(_:)` 方法在 SwiftUI 中实现拖动操作：

```swift
import SwiftUI

struct DragExampleView: View {
    var body: some View {
        VStack {
            Text("拖动这段文本")
                .padding()
                .background(Color.yellow)
                .cornerRadius(10)
                // 使用 onDrag 来指定拖动时提供的数据
                .onDrag {
                    // 创建 NSItemProvider，提供拖动时的数据
                    return NSItemProvider(object: NSString(string: "这是拖动的文本"))
                }

            Image(systemName: "star.fill")
                .resizable()
                .frame(width: 100, height: 100)
                .foregroundColor(.blue)
                .onDrag {
                    // 使用 NSItemProvider 提供图片的拖动数据
                    return NSItemProvider(object: UIImage(systemName: "star.fill")!)
                }
        }
        .padding()
    }
}

struct DragExampleView_Previews: PreviewProvider {
    static var previews: some View {
        DragExampleView()
    }
}
```

#### 代码说明：

* `Text("拖动这段文本")`：我们使用了 `onDrag` 修饰符，指定在拖动文本时提供 `NSString` 类型的文本数据，用户可以拖动这段文本到其他支持文本输入的地方。
* `Image(systemName: "star.fill")`：这是一个系统图标星形图像，使用 `onDrag` 来提供图像数据，用户可以拖动该图像。

#### 运行效果：

1. 用户可以从应用中拖动文本 "拖动这段文本" 到支持文本输入的地方。
2. 用户可以从应用中拖动星形图标到支持图片接收的地方。
