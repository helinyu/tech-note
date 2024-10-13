# iOS简单例子

在 iOS 开发中，MVP 模式可以有效地将视图和业务逻辑分离。以下是一个简单的 MVP 模式示例，其中包括 `View`、`Presenter` 和 `Model`，用于展示用户登录流程。

#### 1. Model

`Model` 是数据的提供者。在这个例子中，它提供登录验证逻辑。

```swift
struct User {
    let username: String
    let password: String
}

class AuthService {
    func login(user: User, completion: @escaping (Bool) -> Void) {
        // 模拟网络请求的异步处理
        DispatchQueue.global().asyncAfter(deadline: .now() + 1.0) {
            // 简单验证逻辑：用户名和密码都等于 "admin" 时返回成功
            let isSuccess = (user.username == "admin" && user.password == "admin")
            completion(isSuccess)
        }
    }
}
```

#### 2. View

`View` 是展示层。它包含 UI 元素，如文本输入框和按钮。在 MVP 中，`View` 通过接口与 `Presenter` 交互。

```swift
protocol LoginView: AnyObject {
    func showLoading()
    func hideLoading()
    func showLoginSuccess()
    func showLoginFailure()
}

class LoginViewController: UIViewController, LoginView {
    private let presenter = LoginPresenter(authService: AuthService())
    
    override func viewDidLoad() {
        super.viewDidLoad()
        presenter.attachView(self) // 关联 Presenter
    }
    
    @IBOutlet weak var usernameTextField: UITextField!
    @IBOutlet weak var passwordTextField: UITextField!
    
    @IBAction func loginButtonTapped(_ sender: UIButton) {
        guard let username = usernameTextField.text, let password = passwordTextField.text else { return }
        presenter.login(username: username, password: password)
    }
    
    func showLoading() {
        // 显示加载指示器
    }
    
    func hideLoading() {
        // 隐藏加载指示器
    }
    
    func showLoginSuccess() {
        // 显示登录成功信息
    }
    
    func showLoginFailure() {
        // 显示登录失败信息
    }
}
```

#### 3. Presenter

`Presenter` 负责处理用户操作，并与 `Model` 交互来获取数据或验证信息。`Presenter` 决定何时通知 `View` 来更新 UI。

```swift
class LoginPresenter {
    private let authService: AuthService
    private weak var view: LoginView?
    
    init(authService: AuthService) {
        self.authService = authService
    }
    
    func attachView(_ view: LoginView) {
        self.view = view
    }
    
    func login(username: String, password: String) {
        view?.showLoading()
        
        let user = User(username: username, password: password)
        authService.login(user: user) { [weak self] isSuccess in
            DispatchQueue.main.async {
                self?.view?.hideLoading()
                if isSuccess {
                    self?.view?.showLoginSuccess()
                } else {
                    self?.view?.showLoginFailure()
                }
            }
        }
    }
}
```

#### 数据流概述

1. 用户在 `View` 中输入用户名和密码，并点击登录按钮。
2. `View` 调用 `Presenter` 的 `login` 方法，传入用户名和密码。
3. `Presenter` 调用 `Model` 的 `login` 方法，开始验证。
4. `Model` 返回验证结果给 `Presenter`。
5. `Presenter` 调用 `View` 的方法，更新 UI 以展示结果（登录成功或失败）。

通过这种方式，业务逻辑都集中在 `Presenter` 中，`View` 仅负责 UI 展示，`Model` 仅负责数据处理和业务逻辑，从而实现良好的解耦。
