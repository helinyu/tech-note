# @StateObject、@ObservedObject、 @EnvironmentObject

`@StateObject`、`@ObservedObject` 和 `@EnvironmentObject` 都是 SwiftUI 中用于处理可观察对象（`ObservableObject`）的属性包装器，它们之间的关系与区别如下：

#### 1. @StateObject

* **定义**：用于在视图中创建并持有一个新的可观察对象实例。
* **生命周期**：只在视图首次加载时创建一次。视图重新加载时不会重新创建该对象。
* **用途**：适用于视图内部需要管理状态的情况。
*   **示例**：

    ```swift
    class MyModel: ObservableObject {
        @Published var value: String = "Initial"
    }

    struct MyView: View {
        @StateObject private var model = MyModel() // 创建并持有

        var body: some View {
            Text(model.value)
        }
    }
    ```

#### 2. @ObservedObject

* **定义**：用于在视图中观察一个已经存在的可观察对象实例。
* **生命周期**：不会创建新的对象，视图会保持对外部对象的引用。
* **用途**：适用于需要在子视图中使用已存在的模型的情况。
*   **示例**：

    ```swift
    struct MyView: View {
        @ObservedObject var model: MyModel // 观察外部对象

        var body: some View {
            Text(model.value)
        }
    }
    ```

#### 3. @EnvironmentObject

* **定义**：用于在视图树中注入和访问一个可观察对象。它通过环境（environment）传递，所有子视图都可以访问。
* **生命周期**：需要在视图树的某个上层视图中通过 `.environmentObject()` 方法提供。
* **用途**：适用于需要在多个层级的视图中共享状态的情况。
*   **示例**：

    ```swift
    struct ParentView: View {
        @StateObject private var model = MyModel()

        var body: some View {
            ChildView()
                .environmentObject(model) // 提供环境对象
        }
    }

    struct ChildView: View {
        @EnvironmentObject var model: MyModel // 访问环境对象

        var body: some View {
            Text(model.value)
        }
    }
    ```

#### 总结

* **@StateObject**：创建并管理对象，适合视图内部使用。
* **@ObservedObject**：观察外部对象，适合子视图使用已存在的对象。
* **@EnvironmentObject**：通过环境传递对象，适合在多个视图层级中共享状态。

通过合理使用这三种属性包装器，可以有效地管理 SwiftUI 应用中的状态和数据流。



<table><thead><tr><th width="132">特性</th><th>@StateObject</th><th>@ObservedObject</th><th>@EnvironmentObject</th></tr></thead><tbody><tr><td><strong>定义</strong></td><td>创建并持有新的可观察对象实例</td><td>观察已有的可观察对象实例</td><td>通过环境注入可观察对象</td></tr><tr><td><strong>生命周期</strong></td><td>视图首次加载时创建一次</td><td>不创建新对象，仅保持对外部对象的引用</td><td>需要在上层视图中提供</td></tr><tr><td><strong>用途</strong></td><td>适用于视图内部管理状态</td><td>适用于子视图使用已存在的模型</td><td>适用于多个层级视图共享状态</td></tr><tr><td><strong>示例</strong></td><td><code>@StateObject private var model = MyModel()</code></td><td><code>@ObservedObject var model: MyModel</code></td><td><code>@EnvironmentObject var model: MyModel</code></td></tr><tr><td><strong>更新响应</strong></td><td>视图更新时自动响应变化</td><td>视图更新时自动响应观察到的变化</td><td>视图更新时自动响应环境对象变化</td></tr></tbody></table>
