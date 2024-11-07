# 代码示例

[参考代码](https://github.com/hly-code-source/exmaples/tree/main/swift/TESTUI)

### 1、 OC和Swift的相互操作 <a href="#id-1-oc-he-swift-de-xiang-hu-cao-zuo" id="id-1-oc-he-swift-de-xiang-hu-cao-zuo"></a>

创建对应的bridge以及导入xx-swift.h 文件，就可以相互操作了。

### 2、OC跳转到SwiftUI页面 <a href="#id-2oc-tiao-zhuan-dao-swiftui-ye-mian" id="id-2oc-tiao-zhuan-dao-swiftui-ye-mian"></a>

OC代码Copy

```
  UIViewController *vc = [[XXViewController alloc] createTestViewController];
    [self.navigationController pushViewController:vc animated:YES];
```

SwiftUI写的代码

```
import SwiftUI

// 重点是这里要创建一个过渡的类，因为在OC中无法写入UIHostingController文件以及MySwiftUIView定义的文件
@objc
class XXViewController: NSObject{
    @MainActor @objc func createTestViewController() -> UIViewController{
        let vc = UIHostingController(rootView: MySwiftUIView());
        return vc
    }
}

public struct MySwiftUIView: View {
    public var body: some View {
        NavigationLink(destination: UIKitViewController()) {
            Text("Hello from SwiftUI!")
                .font(.largeTitle)
                .padding()
                            
        }
    }
    
}
```

### 3、UIKit的页面跳转到SwiftUI的页面 <a href="#id-3uikit-de-ye-mian-tiao-zhuan-dao-swiftui-de-ye-mian" id="id-3uikit-de-ye-mian-tiao-zhuan-dao-swiftui-de-ye-mian"></a>

上面的代码NavigationLink ， 类似push

需要实现UIViewControllerRepresentable 这个协议，将vc嵌入到里里面。

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

        let btn = UIButton(type: .system)
        btn.frame = CGRect(x: 100, y: 100, width: 100, height: 50)
        btn.backgroundColor = .purple
        self.view.addSubview(btn)
        btn.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)
    }

}
```

### 4、SwiftUI跳转到UIKit

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
