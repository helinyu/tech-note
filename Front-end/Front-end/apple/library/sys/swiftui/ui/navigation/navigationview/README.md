# NavigationView

`NavigationView` 是 SwiftUI 中用于管理导航层次结构的容器视图，通常用于在 iOS 应用中创建带有导航栏的页面结构。它允许用户在多个视图之间进行导航，并在顶部提供一个导航栏，可以包含标题、按钮等元素。

#### 基本用法

在 SwiftUI 中，`NavigationView` 是最常用的布局容器之一，尤其在创建主从结构、详情页等多级页面时非常实用。

#### 示例

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        NavigationView {
            VStack {
                Text("Home Page")
                NavigationLink(destination: DetailView()) {
                    Text("Go to Detail")
                }
            }
            .navigationTitle("Home")
        }
    }
}

struct DetailView: View {
    var body: some View {
        Text("Detail Page")
            .navigationTitle("Detail")
    }
}
```

#### 解释

1. **`NavigationView` 容器**：
   * `NavigationView` 将包裹的内容视图放入导航上下文中，使得视图可以利用导航栏的功能，并能够在多个视图之间进行导航。
2. **`NavigationLink`**：
   * `NavigationLink` 是用于导航的视图，点击该链接可以推动另一个视图（如上例中的 `DetailView`）进入视图层次结构。
   * `destination` 是导航的目标视图。
3. **`navigationTitle`**：
   * `navigationTitle` 设置导航栏的标题。不同页面可以有不同的标题，这样在导航过程中，用户可以看到对应页面的标题。

#### 核心功能

* **导航栏**：`NavigationView` 自带一个导航栏，可以通过 `navigationTitle()` 或 `navigationBarTitle()` 设置标题。
* **导航行为**：可以通过 `NavigationLink` 进行页面之间的切换（推送新视图到堆栈中）。
* **导航栏按钮**：可以在导航栏的左侧或右侧添加按钮（使用 `navigationBarItems()` 方法）。
* **多平台支持**：虽然 `NavigationView` 主要用于 iOS，但它也可以用于 macOS、tvOS 和 watchOS。

#### 进阶用法

1. **自定义导航栏按钮**：

可以在导航栏左右两侧自定义按钮，通常用来实现返回或其他功能：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        NavigationView {
            VStack {
                Text("Home Page")
                NavigationLink(destination: DetailView()) {
                    Text("Go to Detail")
                }
            }
            .navigationTitle("Home")
            .navigationBarItems(trailing: Button("Edit") {
                print("Edit button tapped")
            })
        }
    }
}
```

2. **隐藏导航栏**：

可以通过 `.navigationBarHidden(true)` 隐藏某个视图的导航栏：

```swift
struct DetailView: View {
    var body: some View {
        Text("Detail Page")
            .navigationBarHidden(true)
    }
}
```

3. **自定义返回按钮**：

可以通过 `navigationBarBackButtonHidden(true)` 隐藏系统默认的返回按钮，并自定义一个返回按钮：

```swift
struct DetailView: View {
    @Environment(\.presentationMode) var presentationMode

    var body: some View {
        VStack {
            Text("Detail Page")
            Button("Back") {
                presentationMode.wrappedValue.dismiss()
            }
        }
        .navigationBarBackButtonHidden(true)
    }
}
```

#### 注意点

* **状态管理**：`NavigationView` 依赖视图层次的状态管理，特别是在使用 `@State` 或 `@Binding` 时，要确保状态正确传递，避免导航行为不一致。
* **性能**：在复杂应用中，导航层次过深可能会影响性能，因此应该合理规划视图层次和导航逻辑。

#### 未来发展

随着 iOS 16 及更高版本中引入的 `NavigationStack` 和 `NavigationSplitView`，`NavigationView` 可能逐渐被这些新的导航结构替代。新的组件提供了更灵活和现代化的导航功能，但在当前版本的 SwiftUI 中，`NavigationView` 仍然是最基础和常用的导航工具。

总结来说，`NavigationView` 是 SwiftUI 中用于实现多页面导航的基础视图容器，通过与 `NavigationLink` 配合，可以构建出导航栏和页面堆栈的完整用户体验。
