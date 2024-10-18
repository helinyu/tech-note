# 耦合度

在MVC架构中，降低耦合度对确保组件独立性、可维护性和模块化至关重要。耦合度主要通过分析组件间的依赖关系来识别。以下是如何在MVC中识别和降低耦合度的几个方法：

#### 1. **Model与View的耦合**

**识别方法：** 检查是否有任何视图直接访问或修改了模型的数据。例如，如果视图直接操作模型中的数据而不是通过控制器，这表明耦合度较高。

**降低方法：**

* **使用控制器**作为中介，避免视图直接操作模型。
* **使用数据绑定或通知机制**，如KVO（Key-Value Observing）或通知中心，这样模型状态改变时通知视图更新，而无需直接引用。
* **依赖倒置原则（Dependency Inversion Principle）**：让模型通过协议通知变化，而不是直接与视图耦合。

#### 2. **Controller与View的耦合**

**识别方法：** 查看控制器中是否直接操作了视图的具体属性，如视图的布局、样式或显示逻辑。控制器不应该对视图的具体呈现细节有过多的依赖。

**降低方法：**

* 使用\*\*视图模型（ViewModel）\*\*分离视图的展示逻辑，将视图的状态或配置交给视图模型处理。
* 控制器应该传递**数据和事件**给视图，而不是直接操纵视图的细节，如`UIViewController`与`UIView`之间传递的是更新内容，而不是更新样式。
*   可以通过协议方式定义视图接口，使控制器和视图之间的关系解耦，例如：

    ```swift
    protocol TodoViewProtocol: AnyObject {
        func displayTodos(_ todos: [Todo])
    }

    class TodoViewController: UIViewController, TodoViewProtocol {
        func displayTodos(_ todos: [Todo]) {
            // 更新视图
        }
    }
    ```

#### 3. **Controller与Model的耦合**

**识别方法：** 如果控制器直接修改了模型中的复杂逻辑或规则（如数据验证、业务规则），则表明耦合度较高。

**降低方法：**

* **将业务逻辑放在模型中**，控制器只负责调用模型方法，而不直接操作或包含业务逻辑。
* 使用**服务层或数据管理层**（如Repository），为控制器提供数据访问的接口，避免直接依赖于模型细节。
*   在复杂应用中，可以引入**接口/协议**使控制器与模型的具体实现解耦：

    ```swift
    protocol TodoModelProtocol {
        func fetchTodos() -> [Todo]
    }
    ```

#### 4. **使用依赖注入**

将依赖项通过初始化方法注入，可以降低组件之间的耦合度，使代码更容易测试和扩展。例如，控制器可以通过构造函数注入模型对象，而不是在内部创建它：

```swift
class TodoViewController: UIViewController {
    private let model: TodoModelProtocol

    init(model: TodoModelProtocol) {
        self.model = model
        super.init(nibName: nil, bundle: nil)
    }
}
```

#### 5. **保持单一责任**

确保每个组件只负责一项任务，这样可以降低相互依赖的可能性。例如，控制器只负责协调模型和视图，不应该包含数据操作的逻辑，而视图也不应该包含业务逻辑。

#### 总结

在MVC中可以通过**避免直接引用、协议抽象、依赖注入**和**职责分离**等方法来识别和减少组件间的耦合度。
