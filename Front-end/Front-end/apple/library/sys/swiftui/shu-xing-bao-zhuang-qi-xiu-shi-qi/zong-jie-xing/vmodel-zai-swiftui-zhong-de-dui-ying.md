# v-model在SwiftUI中的对应

在 SwiftUI 中，`v-model` 的功能主要通过 `@State` 和 `@Binding` 结合使用来实现。这两个属性包装器共同工作，允许你在视图之间创建类似于 Vue 的双向数据绑定。

#### 具体对比

*   **@State**:

    * 用于在一个视图中声明和管理局部状态。它可以让视图在状态变化时自动更新。

    ```swift
    struct ParentView: View {
        @State private var textValue: String = ""
        
        var body: some View {
            TextField("Enter text", text: $textValue)
        }
    }
    ```
*   **@Binding**:

    * 用于在父视图和子视图之间共享状态，使得子视图可以修改父视图的状态，从而实现双向绑定。

    ```swift
    struct ChildView: View {
        @Binding var textValue: String
        
        var body: some View {
            TextField("Child TextField", text: $textValue)
        }
    }
    ```

#### 示例结合

如果你有一个父视图和子视图，你可以这样实现类似于 `v-model` 的效果：

```swift
struct ParentView: View {
    @State private var inputText: String = ""
    
    var body: some View {
        VStack {
            TextField("Parent TextField", text: $inputText)
            ChildView(textValue: $inputText)
        }
    }
}

struct ChildView: View {
    @Binding var textValue: String
    
    var body: some View {
        TextField("Child TextField", text: $textValue)
    }
}
```

在这个示例中，`ParentView` 中的 `inputText` 状态可以通过 `TextField` 和 `ChildView` 中的 `TextField` 进行双向绑定，类似于 Vue 中的 `v-model` 功能。
