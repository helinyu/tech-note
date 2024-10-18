# iOS的简单示例

在iOS中，MVC（Model-View-Controller）是一种常见的软件设计模式，它通过将应用程序分成三个主要组件来帮助管理复杂性：模型、视图和控制器。下面是一个简单的MVC示例，展示了如何在iOS中实现这个模式。

#### 示例：简单的待办事项列表

**1. 模型（Model）**

模型表示应用程序的数据和业务逻辑。在这个例子中，我们将创建一个待办事项（Todo）模型。

```swift
struct Todo {
    var title: String
    var isCompleted: Bool
}
```

**2. 视图（View）**

视图负责显示模型的数据。在这个例子中，我们将使用`UITableView`来显示待办事项。

```swift
import UIKit

class TodoViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
    
    var todos: [Todo] = [
        Todo(title: "Buy groceries", isCompleted: false),
        Todo(title: "Walk the dog", isCompleted: false),
        Todo(title: "Read a book", isCompleted: true)
    ]
    
    let tableView = UITableView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        title = "Todos"
        view.addSubview(tableView)
        tableView.frame = view.bounds
        tableView.dataSource = self
        tableView.delegate = self
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return todos.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        let todo = todos[indexPath.row]
        cell.textLabel?.text = todo.title
        cell.accessoryType = todo.isCompleted ? .checkmark : .none
        return cell
    }
}
```

**3. 控制器（Controller）**

控制器是模型和视图之间的桥梁，负责协调它们的交互。在这个例子中，`TodoViewController`充当控制器。

```swift
// 控制器代码在上面的 TodoViewController 中已经包含

override func viewDidLoad() {
    super.viewDidLoad()
    // 初始化数据和视图
}
```

#### 总结

这个简单的待办事项列表应用程序展示了MVC设计模式在iOS中的基本应用。模型`Todo`表示待办事项的数据，视图`TodoViewController`显示这些数据，而控制器则负责协调模型和视图之间的交互。在实际应用中，MVC模式可以进一步扩展和细化，以适应更复杂的需求。
