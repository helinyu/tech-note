# 2、在SWiftUI项目中引入xcframework库

在 SwiftUI 中使用自定义的 XCFramework 非常简单。以下是将你创建的 XCFramework 集成到 SwiftUI 项目中的详细步骤和代码示例：

***

#### 1. **将 XCFramework 添加到项目**

1. 打开你的 SwiftUI 项目。
2. 将生成的 `MyFramework.xcframework` 文件拖入 Xcode 项目的 **Project Navigator**。
3. 确保选中 "Copy items if needed" 选项。
4. 在项目的 **"General" > Frameworks, Libraries, and Embedded Content** 部分，确认 `MyFramework.xcframework` 已添加。

***

#### 2. **在 SwiftUI 中导入 XCFramework**

在需要使用的 SwiftUI 视图中，导入 `MyFramework` 并调用其方法。

**示例：**

```swift
import SwiftUI
import MyFramework  // 导入自定义 XCFramework

struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, SwiftUI!")
                .padding()
            
            Button(action: {
                MyFramework.sayHello()  // 调用 XCFramework 的方法
            }) {
                Text("Call Framework")
                    .foregroundColor(.white)
                    .padding()
                    .background(Color.blue)
                    .cornerRadius(8)
            }
        }
    }
}
```

***

#### 3. **运行并测试**

1. 运行你的 SwiftUI 应用程序。
2. 点击 **"Call Framework"** 按钮，应该会在 Xcode 控制台中看到 `Hello from MyFramework!` 的输出。

***

#### 4. **扩展框架功能（可选）**

如果你的 XCFramework 提供了更多的功能，比如返回字符串数据或与 UI 集成，可以将结果与 SwiftUI 的视图绑定。例如：

**更新 MyFramework.swift：**

```swift
import Foundation

public class MyFramework {
    public static func fetchMessage() -> String {
        return "Hello from MyFramework!"
    }
}
```

**在 SwiftUI 中使用返回值：**

```swift
import SwiftUI
import MyFramework

struct ContentView: View {
    @State private var message: String = "Default Message"

    var body: some View {
        VStack {
            Text(message)
                .padding()
            
            Button(action: {
                message = MyFramework.fetchMessage()  // 更新视图绑定的状态
            }) {
                Text("Fetch Message")
                    .foregroundColor(.white)
                    .padding()
                    .background(Color.green)
                    .cornerRadius(8)
            }
        }
    }
}
```

在这个例子中，点击按钮后，XCFramework 的返回值会更新 SwiftUI 界面。

***

#### 5. **支持实时预览**

在使用 SwiftUI 的实时预览时，确保你的 XCFramework 支持目标平台（如 iOS Simulator）。如果框架仅为设备架构构建（如 `arm64`），预览可能无法正常工作。为了避免问题，请确认在创建 XCFramework 时包含模拟器架构（`x86_64` 和 `arm64`）。

***

#### 总结

在 SwiftUI 中使用 XCFramework 与在普通项目中类似，只需导入框架并调用其中的方法。

