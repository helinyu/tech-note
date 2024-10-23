# @StateObject

`@StateObject` 是 SwiftUI 中用于<mark style="color:red;">**管理状态**</mark>的一种属性包装器，适用于在视图中创建并持有一个新的可观察对象（`ObservableObject`）的实例。`@StateObject` 的主要特点和使用方法如下：

#### 特点

1. **持有对象**：`@StateObject` 会在视图的生命周期内持有一个 `ObservableObject` 实例，确保其状态在视图重新加载时不会丢失。
2. **自动更新**：当 `ObservableObject` 中的任何 `@Published` 属性发生变化时，依赖于该对象的视图会自动更新。
3. **适合初始创建**：通常在视图的 `init` 方法或直接在视图声明时创建 `@StateObject`，<mark style="color:red;">确保它只在视图的第一次加载时创建一次</mark>。

#### 使用示例

以下是一个使用 `@StateObject` 的简单示例：

```swift
import SwiftUI

// 模型
class CounterModel: ObservableObject {
    @Published var count: Int = 0 // 被观察的属性

    func increment() {
        count += 1 // 更新计数
    }
}

struct ContentView: View {
    @StateObject private var counter = CounterModel() // 创建并持有 CounterModel 实例

    var body: some View {
        VStack {
            Text("Count: \(counter.count)") // 显示当前计数
                .font(.largeTitle)

            Button("Increment") {
                counter.increment() // 调用模型的方法来增加计数
            }
            .padding()
            .background(Color.blue)
            .foregroundColor(.white)
            .cornerRadius(8)
        }
        .padding()
    }
}
```

#### 说明

1. **模型定义**：`CounterModel` 类实现了 `ObservableObject` 协议，包含一个被 `@Published` 修饰的 `count` 属性和一个增加计数的方法 `increment()`。
2. **视图定义**：`ContentView` 使用 `@StateObject` 创建并持有 `CounterModel` 的实例。当按钮被点击时，`increment()` 方法会更新 `count` 的值。
3. **自动更新**：当 `count` 发生变化时，`ContentView` 中的 `Text` 会自动更新，显示最新的计数。

#### 何时使用 @StateObject

* 当你需要在视图中创建一个新的可观察对象时，使用 `@StateObject`。
* 如果你已经有一个可观察对象并希望在子视图中使用，应该使用 `@ObservedObject` 或 `@EnvironmentObject`。

通过 `@StateObject`，SwiftUI 提供了一种简单且高效的方式来管理和响应视图状态的变化。
