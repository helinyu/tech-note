# @binding

<mark style="color:red;">这个绑定是父子组件之间的绑定。  和</mark>[ <mark style="color:red;">model与view之间的双向绑定</mark>](shuang-xiang-bang-ding-publish-binding-observedobject-observedobject.md)<mark style="color:red;">是有区别的。 不过也是要用到@binding的。</mark>



1. **父视图可以更新子视图的状态**：当父视图的状态（`@State` 或其他状态管理）发生变化时，绑定到子视图的 `@Binding` 属性会自动更新，从而更新子视图的显示。
2. **子视图可以更新父视图的状态**：子视图中对 `@Binding` 属性的修改会直接反映到父视图中，这样父视图的状态也会随之改变。

下面是一个示例来说明这一点：

```swift
import SwiftUI

struct ParentView: View {
    @State private var text: String = "Initial Text"

    var body: some View {
        VStack {
            ChildView(text: $text) // 传递绑定

            Text("Parent Text: \(text)") // 显示父视图的文本
                .padding()
        }
    }
}

struct ChildView: View {
    @Binding var text: String // 使用 @Binding 接收父视图的状态

    var body: some View {
        VStack {
            TextField("Enter text", text: $text) // 修改 @Binding 会更新父视图的状态
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .padding()

            Button("Change Parent Text") {
                text = "Updated from Child" // 更新 @Binding 会反映到父视图
            }
        }
    }
}
```

在这个例子中，`ChildView` 使用了 `@Binding` 来接收来自 `ParentView` 的 `text` 状态。当在子视图中修改 `text` 时，父视图也会实时更新显示的文本。
