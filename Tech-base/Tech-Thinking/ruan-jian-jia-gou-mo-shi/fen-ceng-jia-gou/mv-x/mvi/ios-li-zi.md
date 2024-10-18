# iOS例子

展示如何使用 Swift 创建一个简单的计数器应用。该应用允许用户增加或减少计数。

#### 项目结构

1. **Model**：存储应用的状态。
2. **View**：负责用户界面。
3. **Intent**：表示用户的操作。
4. **Intent Processor**：处理用户的 Intent 并更新 Model。

#### 代码示例

**1. Model**

```swift
// CounterModel.swift
struct CounterModel {
    let count: Int
}
```

**2. Intent**

```swift
// CounterIntent.swift
enum CounterIntent {
    case increment
    case decrement
}
```

**3. Intent Processor**

```swift
// CounterViewModel.swift
import Combine

class CounterViewModel: ObservableObject {
    @Published private(set) var model: CounterModel = CounterModel(count: 0)
    
    func processIntent(_ intent: CounterIntent) {
        switch intent {
        case .increment:
            model = CounterModel(count: model.count + 1)
        case .decrement:
            model = CounterModel(count: model.count - 1)
        }
    }
}
```

**4. View**

```swift
// ContentView.swift
import SwiftUI

struct ContentView: View {
    @ObservedObject var viewModel = CounterViewModel()

    var body: some View {
        VStack {
            Text("Count: \(viewModel.model.count)")
                .font(.largeTitle)
                .padding()

            HStack {
                Button(action: {
                    viewModel.processIntent(.increment)
                }) {
                    Text("Increment")
                        .padding()
                        .background(Color.green)
                        .foregroundColor(.white)
                        .cornerRadius(8)
                }

                Button(action: {
                    viewModel.processIntent(.decrement)
                }) {
                    Text("Decrement")
                        .padding()
                        .background(Color.red)
                        .foregroundColor(.white)
                        .cornerRadius(8)
                }
            }
        }
        .padding()
    }
}
```

**5. 主应用程序**

```swift
// MyApp.swift
import SwiftUI

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

#### 代码说明

* **Model**：`CounterModel` 存储计数的值。
* **Intent**：`CounterIntent` 定义了用户可以执行的操作（增减计数）。
* **Intent Processor**：`CounterViewModel` 处理用户的 Intent，并根据 Intent 更新 Model 的状态。
* **View**：`ContentView` 显示当前计数，并提供增减按钮，按钮点击后会调用 ViewModel 的 `processIntent` 方法。

#### 运行应用

1. 创建一个新的 SwiftUI 项目。
2. 替换默认的代码为上面的示例代码。
3. 运行应用，您将看到一个简单的计数器界面，可以通过按钮增减计数。

这个简单的例子展示了如何使用 MVI 架构在 iOS 中实现用户界面和状态管理，保持了清晰的结构和单向数据流。
