# @state vs @binding

`@State` 和 `@Binding` 是 SwiftUI 中用于管理状态的两种不同属性包装器。

#### @State

* **用途**: 用于在视图中声明和管理局部状态。
* **作用域**: 仅在声明它的视图内有效。
*   **示例**: 当你想要一个视图自己管理的状态，例如一个按钮的点击计数。

    ```swift
    struct CounterView: View {
        @State private var count = 0
        
        var body: some View {
            VStack {
                Text("Count: \(count)")
                Button("Increment") {
                    count += 1
                }
            }
        }
    }
    ```

#### @Binding

* **用途**: 用于在父视图和子视图之间共享状态。
* **作用域**: 允许子视图访问和修改父视图的状态。
*   **示例**: 当你想让子视图能够修改父视图的状态，例如一个切换开关。

    ```swift
    struct ParentView: View {
        @State private var isOn = false
        
        var body: some View {
            ToggleView(isOn: $isOn)
        }
    }

    struct ToggleView: View {
        @Binding var isOn: Bool
        
        var body: some View {
            Toggle("Toggle Me", isOn: $isOn)
        }
    }
    ```

#### 总结

* 使用 `@State` 管理局部状态，使用 `@Binding` 在视图之间共享和修改状态。

下面是 `@State` 和 `@Binding` 的对比表格：

| 属性包装器      | 用途             | 作用域          | 示例                             |
| ---------- | -------------- | ------------ | ------------------------------ |
| `@State`   | 管理局部状态         | 仅在声明的视图内有效   | `@State private var count = 0` |
| `@Binding` | 在父视图和子视图之间共享状态 | 允许子视图访问父视图状态 | `@Binding var isOn: Bool`      |

#### 详细说明

* **@State**: 用于创建和管理一个视图的局部状态，视图会在状态变化时自动重新渲染。
* **@Binding**: 用于让子视图能够访问和修改父视图的状态，从而实现状态共享。
