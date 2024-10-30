# Form



在SwiftUI中，`Form` 是一个用于创建可滚动的表单的容器，它适合用于<mark style="color:red;">**输入数据和设置**</mark>。`Form` 可以包含各种控件，如文本字段、开关、选择器等，便于用户输入和选择。

其实就是和其他的UI的表单是一样的，表单有什么特性。



```swift
import SwiftUI

struct ContentView: View {
    @State private var name: String = ""
    @State private var age: String = ""
    @State private var isSubscribed: Bool = false

    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Personal Information")) {
                    TextField("Name", text: $name)
                    TextField("Age", text: $age)
                }
                
                Section {
                    Toggle(isOn: $isSubscribed) {
                        Text("Subscribe to newsletter")
                    }
                }
                
                Section {
                    Button(action: {
                        // 提交表单的逻辑
                    }) {
                        Text("Submit")
                    }
                }
            }
            .navigationTitle("User Form")
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

#### 主要组件：

* **TextField**：用于输入文本。
* **Toggle**：用于开关选项。
* **Button**：用于执行操作，如提交表单。

#### 使用场景：

* 用户注册或登录。
* 设置页面。
* 数据收集表单。

`Form` 也支持分组（Section），使得不同类型的输入更有组织性。你可以根据需要添加更多控件来扩展功能！如果你有具体的需求或问题，欢迎提问！
