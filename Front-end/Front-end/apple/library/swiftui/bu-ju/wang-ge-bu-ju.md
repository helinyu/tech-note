# 网格布局

在 SwiftUI 中，`LazyVGrid` 和 `LazyHGrid` 用于实现网格布局。与 `VStack` 和 `HStack` 不同，`LazyVGrid` 和 `LazyHGrid` 会按需懒加载内容，仅渲染当前可见区域内的项目，从而优化性能，特别是在显示大量项目时。

#### 1. 使用 `LazyVGrid` 实现垂直网格

`LazyVGrid` 适用于在垂直方向排列网格项目，并且允许你定义列的布局规则。

**基本示例**

```swift
struct GridExample: View {
    let columns = [
        GridItem(.fixed(100)),  // 固定列宽
        GridItem(.flexible()),  // 灵活列宽
        GridItem(.adaptive(minimum: 50))  // 自适应列宽
    ]
    
    var body: some View {
        ScrollView {
            LazyVGrid(columns: columns, spacing: 20) {
                ForEach(0..<50) { index in
                    Text("Item \(index)")
                        .frame(height: 100)
                        .background(Color.blue)
                        .cornerRadius(8)
                }
            }
            .padding()
        }
    }
}
```

在这个示例中，我们使用了 `LazyVGrid`，并通过 `columns` 参数定义了列的布局：

* 第一列的宽度是固定的，100 点。
* 第二列的宽度是灵活的，会根据屏幕大小自适应调整。
* 第三列是自适应的，最小宽度为 50 点，尽量多放列。

`LazyVGrid` 会在垂直方向生成网格，并将列布局应用到每一行。

#### 2. 使用 `LazyHGrid` 实现水平网格

`LazyHGrid` 适用于在水平方向排列网格项目，类似 `LazyVGrid`，但网格会按行排列。

**基本示例**

```swift
struct HorizontalGridExample: View {
    let rows = [
        GridItem(.fixed(100)),  // 固定行高
        GridItem(.flexible()),  // 灵活行高
        GridItem(.adaptive(minimum: 50))  // 自适应行高
    ]
    
    var body: some View {
        ScrollView(.horizontal) {
            LazyHGrid(rows: rows, spacing: 20) {
                ForEach(0..<50) { index in
                    Text("Item \(index)")
                        .frame(width: 100)
                        .background(Color.green)
                        .cornerRadius(8)
                }
            }
            .padding()
        }
    }
}
```

这里，我们定义了行的布局规则：

* 第一行的高度是固定的 100 点。
* 第二行的高度是灵活的，会根据可用空间自适应。
* 第三行是自适应的，最小高度为 50 点。

`LazyHGrid` 将内容在水平方向滚动，并使用行布局。

#### 3. 自适应网格 (`.adaptive`)

`.adaptive` 允许你设置项目的最小宽度或高度，并根据容器的可用空间动态调整项目的数量，确保它们尽可能多地填充容器。

```swift
struct AdaptiveGridExample: View {
    let columns = [
        GridItem(.adaptive(minimum: 80))
    ]
    
    var body: some View {
        ScrollView {
            LazyVGrid(columns: columns, spacing: 20) {
                ForEach(0..<100) { index in
                    Text("Item \(index)")
                        .frame(width: 80, height: 80)
                        .background(Color.purple)
                        .cornerRadius(8)
                }
            }
            .padding()
        }
    }
}
```

在这个示例中，每个网格项的最小宽度为 80 点，但当屏幕宽度足够时，更多的项目可以被放入同一行。这使得布局非常灵活，可以根据设备屏幕宽度调整列数。

#### 4. 自定义网格项间距

你可以通过 `spacing` 属性来调整网格项目之间的间距：

```swift
let columns = [
    GridItem(.fixed(100), spacing: 10),  // 列间距为 10 点
    GridItem(.flexible(), spacing: 20),  // 列间距为 20 点
    GridItem(.adaptive(minimum: 80), spacing: 30)  // 列间距为 30 点
]
```

这样，你可以控制网格项目之间的距离，使布局更灵活。

#### 总结

* `LazyVGrid` 和 `LazyHGrid` 适用于网格布局，分别用于垂直和水平方向。
* 你可以使用 `.fixed`、`.flexible` 和 `.adaptive` 来灵活定义网格的列或行布局。
* 它们按需渲染内容，适合处理大量项目时优化性能。
