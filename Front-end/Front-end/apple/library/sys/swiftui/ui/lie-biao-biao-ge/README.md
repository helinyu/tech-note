# 列表/表格

在 SwiftUI 中，`Table` 组件用于创建类似于 UIKit 中 `UITableView` 的表格视图。`Table` 允许你以行和列的方式展示数据，适合展示复杂的列表或表格数据。以下是如何在 SwiftUI 中使用 `Table` 的基本示例和功能介绍。

#### 1. 基本用法

```swift
import SwiftUI

struct ContentView: View {
    let items = ["Item 1", "Item 2", "Item 3", "Item 4"]

    var body: some View {
        Table(items, id: \.self) {
            TableColumn("Items") { item in
                Text(item)
            }
        }
    }
}
```

在这个示例中，我们创建了一个简单的 `Table`，并用一个字符串数组作为数据源。`TableColumn` 定义了每一列的标题和内容。

#### 2. 使用模型数据

通常情况下，您可能会使用模型数据而不是简单的字符串数组。以下是使用结构体作为数据模型的示例：

```swift
struct Item: Identifiable {
    var id = UUID()
    var name: String
    var description: String
}

struct ContentView: View {
    let items = [
        Item(name: "Item 1", description: "Description 1"),
        Item(name: "Item 2", description: "Description 2"),
        Item(name: "Item 3", description: "Description 3")
    ]

    var body: some View {
        Table(items) {
            TableColumn("Name", value: \.name)
            TableColumn("Description", value: \.description)
        }
    }
}
```

在这个示例中，我们定义了一个 `Item` 结构体，并使用 `Identifiable` 协议来标识每个项目。`TableColumn` 可以通过 `value:` 参数直接绑定到模型属性。

#### 3. 增加交互功能

可以为 `Table` 添加行选择、删除和编辑功能。以下是一个添加行选择功能的示例：

```swift
struct ContentView: View {
    @State private var selectedItem: Item?

    let items = [
        Item(name: "Item 1", description: "Description 1"),
        Item(name: "Item 2", description: "Description 2"),
        Item(name: "Item 3", description: "Description 3")
    ]

    var body: some View {
        Table(items, selection: $selectedItem) {
            TableColumn("Name", value: \.name)
            TableColumn("Description", value: \.description)
        }
        .onChange(of: selectedItem) { newItem in
            if let item = newItem {
                print("Selected item: \(item.name)")
            }
        }
    }
}
```

在这个示例中，我们使用 `@State` 属性包装器来存储选中的项目，并在选择发生变化时执行操作。

#### 4. 表格行的删除功能

要实现删除功能，可以使用 `onDelete` 修饰符，允许用户通过滑动手势删除行：

```swift
struct ContentView: View {
    @State private var items = [
        Item(name: "Item 1", description: "Description 1"),
        Item(name: "Item 2", description: "Description 2"),
        Item(name: "Item 3", description: "Description 3")
    ]

    var body: some View {
        Table(items) {
            TableColumn("Name", value: \.name)
            TableColumn("Description", value: \.description)
        }
        .onDelete { indexSet in
            items.remove(atOffsets: indexSet)
        }
    }
}
```

在这里，我们使用 `onDelete` 修饰符来响应用户删除行的操作。

#### 5. 自定义行视图

你还可以自定义行的视图，以便在每行中展示更复杂的 UI 元素：

```swift
struct ContentView: View {
    let items = [
        Item(name: "Item 1", description: "Description 1"),
        Item(name: "Item 2", description: "Description 2"),
        Item(name: "Item 3", description: "Description 3")
    ]

    var body: some View {
        Table(items) {
            TableColumn("Name") { item in
                HStack {
                    Image(systemName: "star")
                    Text(item.name)
                }
            }
            TableColumn("Description", value: \.description)
        }
    }
}
```

在这个示例中，我们在表格的“Name”列中添加了一个图标，以创建更具视觉吸引力的行。

#### 总结

* `Table` 是 SwiftUI 中用于创建表格视图的组件，支持行和列的布局。
* 使用 `TableColumn` 定义列，支持绑定到模型数据。
* 可添加交互功能，如选择、删除等。
* 支持自定义行视图，以显示更复杂的内容。

这些功能使得 `Table` 成为在 SwiftUI 应用中展示结构化数据的强大工具。
