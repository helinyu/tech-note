# @SceneStorage

`@SceneStorage` 是 SwiftUI 中用于自动保存和恢复视图状态的属性包装器。它帮助你在场景（Scene）的<mark style="color:orange;">生命周期内保持视图的某些状态信息，例如选中的标签、输入的文本或其他可以序列化为</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`UserDefaults`</mark> <mark style="color:orange;"></mark><mark style="color:orange;">支持的简单数据类型。</mark>通过 `@SceneStorage`，你可以简化状态管理，而无需手动保存和恢复这些状态。

#### `@SceneStorage` 主要特性

1. **自动状态保存和恢复**：当场景被挂起、关闭或重新激活时，标记的状态值会被自动保存和恢复，确保用户的操作状态在应用生命周期内得到保存。
2. **基于键值存储**：`@SceneStorage` 使用键值对方式保存数据，需要你提供一个唯一的字符串键。这个键可以在整个应用的不同视图中保持一致，从而共享数据。
3. **支持的数据类型**：`@SceneStorage` 只支持一些基础类型的数据，比如 `Int`、`String`、`Double`、`Bool` 等可以被 `UserDefaults` 序列化的类型。如果要存储更复杂的类型，需要自己处理序列化。

#### 使用场景

`@SceneStorage` 通常用于保存视图的短期状态，比如：

* 当前选择的选项
* 滚动位置
* 输入框的文本内容
* 临时表单数据

这类数据不需要长期存储到磁盘，但在应用的使用期间，用户希望它们能保持一致。

#### 代码示例

以下是使用 `@SceneStorage` 的一个示例，展示如何保存用户选中的文本信息：

```swift
import SwiftUI

struct ContentView: View {
    @SceneStorage("userInput") private var userInput: String = ""

    var body: some View {
        VStack {
            TextField("Enter something", text: $userInput)
                .padding()
                .textFieldStyle(RoundedBorderTextFieldStyle())

            Text("You typed: \(userInput)")
        }
        .padding()
    }
}
```

#### 解释

1. **`@SceneStorage("userInput")`**:
   * 通过 `@SceneStorage` 使用键 `"userInput"` 来保存文本框的输入内容。此键用于唯一标识存储的数据。
2. **`private var userInput: String = ""`**:
   * `userInput` 是一个字符串，表示用户输入的内容。初始值为空字符串。
3. **自动保存和恢复**：
   * 当用户在文本框中输入内容时，`userInput` 的值会自动保存在场景存储中。如果应用被关闭或重新启动，`userInput` 的内容会自动恢复，确保用户之前的输入保持不变。

#### 关键点

* **自动持久化**：`@SceneStorage` 自动将数据保存到 `UserDefaults`，但仅限于场景的生命周期。这意味着即使应用被系统终止，用户的某些操作状态也能恢复。
* **适用类型**：仅支持原生的基础类型。复杂对象无法直接存储，必须先序列化为支持的类型（如 `String` 或 `Data`）。
* **简化状态管理**：无需手动管理状态保存和恢复，适用于需要在短时间内保持用户交互的应用场景。

`@SceneStorage` 是简化 SwiftUI 应用中状态管理的实用工具，适合处理不需要长期保存但希望在场景切换或应用重启时保留的数据。
