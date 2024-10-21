# 导航

**`NavigationView` 和 `NavigationLink`**： 通过 `NavigationView` 和 `NavigationLink` 创建层级结构的导航。尽管没有显式的路由管理，但你可以通过状态来控制导航。

`NavigationView 显示导航栏`

`NavigationLink 导航跳转`



如果导航到UIkit的页面的时候，需要实现UIViewControllerRepresentable 的方法。

```
    NavigationLink(destination: UIKitViewController()) {
                   Text("Go to UIKit View")
                      
  }
  // 导航到UIKitViewController 页面

```

```
import UIKit
import SwiftUI

// 将 UIKit 的视图控制器嵌入 SwiftUI
struct UIKitViewController: UIViewControllerRepresentable {
    // 使用 SwiftUI 的上下文创建和配置 UIKit 控制器
    func makeUIViewController(context: Context) -> some UIViewController {
        // 这里可以是你想要的任何 UIKit 视图控制器
        return TestViewController() // 自定义的 UIViewController
    }

    func updateUIViewController(_ uiViewController: UIViewControllerType, context: Context) {
        // 可以在需要时更新视图控制器的状态
    }
}


class TestViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        self.view.backgroundColor = .green
    }


}

```
