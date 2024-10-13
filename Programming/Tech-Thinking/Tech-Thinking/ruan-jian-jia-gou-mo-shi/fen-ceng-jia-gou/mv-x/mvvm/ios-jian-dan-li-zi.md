# iOS简单例子

在 iOS 中，MVVM（Model-View-ViewModel）模式常用于构建具有良好分离结构和可测试性的应用。下面是一个简单的 MVVM 示例，演示如何在 iOS 中实现这个模式。

#### 示例：使用 MVVM 显示用户信息

**1. Model**

首先定义一个 `User` 模型，表示用户的信息。

```swift
struct User {
    let name: String
    let age: Int
}
```

**2. ViewModel**

然后，创建一个 `UserViewModel`，它将与 `User` 模型交互并提供格式化数据给 View。

```swift
import Foundation

class UserViewModel {
    private var user: User
    
    init(user: User) {
        self.user = user
    }
    
    var name: String {
        return user.name
    }
    
    var age: String {
        return "\(user.age) years old"
    }
}
```

**3. View**

接下来，创建一个简单的视图控制器 `UserViewController`，它将展示用户信息。

```swift
import UIKit

class UserViewController: UIViewController {
    
    private var viewModel: UserViewModel!
    
    private let nameLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        return label
    }()
    
    private let ageLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        return label
    }()
    
    // 初始化 ViewModel
    init(viewModel: UserViewModel) {
        self.viewModel = viewModel
        super.init(nibName: nil, bundle: nil)
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
        bindViewModel()
    }
    
    private func setupUI() {
        view.backgroundColor = .white
        view.addSubview(nameLabel)
        view.addSubview(ageLabel)
        
        // 布局设置
        NSLayoutConstraint.activate([
            nameLabel.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            nameLabel.centerYAnchor.constraint(equalTo: view.centerYAnchor),
            ageLabel.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            ageLabel.topAnchor.constraint(equalTo: nameLabel.bottomAnchor, constant: 20)
        ])
    }
    
    private func bindViewModel() {
        nameLabel.text = viewModel.name
        ageLabel.text = viewModel.age
    }
}
```

**4. 使用示例**

最后，在应用的 `SceneDelegate` 或 `AppDelegate` 中实例化 ViewModel 和 ViewController，并展示它。

```swift
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        
        guard let windowScene = scene as? UIWindowScene else { return }
        
        let window = UIWindow(windowScene: windowScene)
        let user = User(name: "Alice", age: 30)
        let viewModel = UserViewModel(user: user)
        let userViewController = UserViewController(viewModel: viewModel)
        
        window.rootViewController = userViewController
        self.window = window
        window.makeKeyAndVisible()
    }
}
```

#### 总结

在这个示例中：

* **Model** 是 `User`，表示用户的基本信息。
* **ViewModel** 是 `UserViewModel`，提供了从 `User` 数据中派生出的属性（如 `name` 和 `age`）。
* **View** 是 `UserViewController`，展示用户信息并与 ViewModel 绑定。

这种结构允许你在 View 和 Model 之间实现清晰的分离，确保可维护性和可测试性。你可以轻松修改 ViewModel 逻辑或 Model 数据结构，而不影响其他部分的实现。
