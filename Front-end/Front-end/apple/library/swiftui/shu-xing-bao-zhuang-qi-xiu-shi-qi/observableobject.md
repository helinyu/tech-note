# @ObservableObject

`@ObservedObject`是SwiftUI中的一个属性包装器，用于在视图中观察外部对象的状态变化。通常用于与`ObservableObject`协议结合使用。以下是一个基本示例：

```swift
import SwiftUI
import Combine

class MyModel: ObservableObject {
    @Published var count = 0
}

struct ContentView: View {
    @ObservedObject var model = MyModel()
    
    var body: some View {
        VStack {
            Text("Count: \(model.count)")
            Button("Increment") {
                model.count += 1
            }
        }
    }
}
```

在这个示例中，`ContentView`观察`MyModel`的状态。当`count`发生变化时，视图会自动更新。你还有其他想了解的细节吗？
