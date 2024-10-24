# 代码示例

下面是一个使用 `SwiftUI` 和 `NSUserActivity` 的完整代码示例，展示如何在 SwiftUI 环境中使用 `NSUserActivity` 来启用 Handoff、深度链接等功能。这个示例展示了一个简单的文章查看界面，支持 Handoff 和通过 URL 恢复活动。

#### ContentView.swift

```swift
import SwiftUI

struct ContentView: View {
    @State private var articleID: String = "12345"
    
    var body: some View {
        NavigationView {
            VStack {
                Text("Viewing Article \(articleID)")
                    .padding()
                    .onAppear {
                        // 设置 NSUserActivity
                        setupUserActivity()
                    }
            }
            .navigationTitle("Article \(articleID)")
        }
    }
    
    private func setupUserActivity() {
        // 创建并配置 NSUserActivity
        let activity = NSUserActivity(activityType: "com.yourapp.viewingPage")
        
        activity.title = "Viewing Article"
        activity.userInfo = ["articleID": articleID]
        
        // 深度链接，若支持从 Web 直接跳转
        activity.webpageURL = URL(string: "https://yourapp.com/articles/\(articleID)")
        
        // 启用 Handoff 和 Spotlight 搜索
        activity.isEligibleForHandoff = true
        activity.isEligibleForSearch = true
        activity.isEligibleForPublicIndexing = true
        
        // 标记当前活动
        activity.becomeCurrent()
    }
}
```

#### SceneDelegate.swift

在 SwiftUI 项目中，我们可以在 `SceneDelegate` 中处理 Handoff 的恢复。

```swift
import UIKit
import SwiftUI

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        let contentView = ContentView()

        if let windowScene = scene as? UIWindowScene {
            let window = UIWindow(windowScene: windowScene)
            window.rootViewController = UIHostingController(rootView: contentView)
            self.window = window
            window.makeKeyAndVisible()
        }
    }

    // 处理 Handoff 恢复活动
    func scene(_ scene: UIScene, continue userActivity: NSUserActivity) {
        if userActivity.activityType == "com.yourapp.viewingPage" {
            if let articleID = userActivity.userInfo?["articleID"] as? String {
                // 可以在此处恢复文章ID并更新 SwiftUI 界面
                if let rootVC = window?.rootViewController as? UIHostingController<ContentView> {
                    rootVC.rootView.articleID = articleID
                }
            }
        }
    }
}
```

#### Info.plist

确保在 `Info.plist` 中正确配置 Handoff 支持：

```xml
<key>NSUserActivityTypes</key>
<array>
    <string>com.yourapp.viewingPage</string>
</array>
```

#### 完整流程说明

1. **`ContentView` 中的 `setupUserActivity` 方法**：在 `onAppear` 中调用，用于创建和配置 `NSUserActivity`，并将其标记为当前活动。这个活动包含文章的 `articleID` 和深度链接。
2. **`SceneDelegate` 中的 `scene(_:continue:)` 方法**：当应用通过 Handoff 或从其他设备恢复时，该方法会被调用。它从 `NSUserActivity` 中提取 `articleID`，并将其更新到 SwiftUI 界面中。

#### 总结

这个代码展示了如何在 SwiftUI 环境下使用 `NSUserActivity` 来启用 Handoff 功能，以及如何在设备之间无缝恢复用户的活动。这种方式可以帮助用户在不同的设备上继续任务，同时保持应用的状态和数据的一致性。
