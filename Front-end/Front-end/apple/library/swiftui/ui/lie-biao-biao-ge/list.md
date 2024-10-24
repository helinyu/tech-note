# List

在 SwiftUI 中，并没有与 UIKit 的 `UITableView` 完全等价的组件，但 SwiftUI 提供了更现代化的 `List` 组件来代替 `UITableView`。`List` 允许你轻松展示可滚动的列表，支持分组、可滑动删除、移动等功能。

#### 1. 基本的 `List` 使用

```swift
struct SimpleListView: View {
    let items = ["Item 1", "Item 2", "Item 3", "Item 4"]

    var body: some View {
        List(items, id: \.self) { item in
            Text(item)
        }
    }
}
```

这个例子展示了如何使用 `List` 显示一个字符串数组。SwiftUI 会自动处理列表的布局和滚动。

#### 2. 自定义行内容

你可以为列表的每一行自定义内容，不局限于 `Text`：

```swift
struct CustomRowListView: View {
    let items = ["Item 1", "Item 2", "Item 3", "Item 4"]

    var body: some View {
        List(items, id: \.self) { item in
            HStack {
                Image(systemName: "star")
                Text(item)
                    .font(.headline)
                Spacer()
                Image(systemName: "chevron.right")
            }
            .padding()
        }
    }
}
```

在这个例子中，每一行不仅包含文本，还包含图片和其他自定义视图。

#### 3. 动态数据源 `List` with `ForEach`

当你有动态数据时，可以结合 `ForEach` 和 `List` 一起使用：

```swift
struct DynamicListView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]

    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

这个 `List` 会随着 `items` 数组的变化自动更新显示。

#### 4. 可删除和移动的列表

SwiftUI 中的 `List` 也支持可滑动删除和移动功能，类似于 `UITableView` 的行为：

**可删除功能：**

```swift
struct DeletableListView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]

    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
            .onDelete(perform: deleteItem)
        }
    }

    func deleteItem(at offsets: IndexSet) {
        items.remove(atOffsets: offsets)
    }
}
```

通过在 `ForEach` 后添加 `.onDelete`，你可以实现滑动删除功能。

**可移动功能：**

```swift
struct MovableListView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]

    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
            .onMove(perform: moveItem)
        }
        .toolbar {
            EditButton()
        }
    }

    func moveItem(from source: IndexSet, to destination: Int) {
        items.move(fromOffsets: source, toOffset: destination)
    }
}
```

这里添加了 `.onMove` 方法，让用户可以在编辑模式下拖动来重新排序列表。`EditButton` 是 SwiftUI 提供的用于切换列表编辑状态的按钮。

#### 5. 分组的 `List`

`List` 也支持分组列表：

```swift
struct GroupedListView: View {
    let groupedItems = [
        "Fruits": ["Apple", "Banana", "Orange"],
        "Vegetables": ["Carrot", "Potato", "Tomato"]
    ]

    var body: some View {
        List {
            ForEach(groupedItems.keys.sorted(), id: \.self) { key in
                Section(header: Text(key)) {
                    ForEach(groupedItems[key]!, id: \.self) { item in
                        Text(item)
                    }
                }
            }
        }
    }
}
```

通过使用 `Section`，你可以在列表中添加分组，并为每一组定义一个标题。

#### 6. 列表的样式

你可以通过 `.listStyle` 修饰符来改变列表的显示样式，例如默认、分组、内嵌样式等：

```swift
List(items, id: \.self) { item in
    Text(item)
}
.listStyle(GroupedListStyle())
```

常见的列表样式包括：

* `.plain`：默认的列表样式。
* `.grouped`：带分组的列表样式。
* `.insetGrouped`：内嵌分组样式，类似于设置页面的样式。

#### 7. 支持复杂的数据模型

`List` 不仅支持简单数据，还支持复杂的数据模型展示：

```swift
struct Person: Identifiable {
    let id = UUID()
    let name: String
    let age: Int
}

struct ComplexListView: View {
    let people = [
        Person(name: "Alice", age: 25),
        Person(name: "Bob", age: 30),
        Person(name: "Charlie", age: 35)
    ]

    var body: some View {
        List(people) { person in
            VStack(alignment: .leading) {
                Text(person.name)
                    .font(.headline)
                Text("Age: \(person.age)")
            }
        }
    }
}
```

在这里，`Person` 是一个符合 `Identifiable` 协议的结构体，用于展示更复杂的数据。

#### 总结

SwiftUI 中的 `List` 提供了替代 UIKit `UITableView` 的现代化解决方案，支持动态数据、分组、滑动删除、移动等功能，并且使用更加简洁且易于理解的声明式语法。
