# iOS系统提供

在 iOS 系统中，虽然没有明确称为“备忘录”的类或模块，但很多系统框架和工具提供了类似 **备忘录设计模式** 的功能，用于保存和恢复对象状态、支持撤销与重做、或实现数据快照功能。以下是 iOS 系统中主要与备忘录模式相关的功能：

***

#### 1. **`UndoManager`**

`UndoManager` 是 iOS 提供的一个撤销和重做管理工具，内置在系统中，可用于跟踪和恢复用户操作。

* **特点**：
  * 自动管理撤销和重做操作的堆栈。
  * 可以保存对象的状态或操作方法，用于支持撤销/重做。
* **使用场景**：
  * 文本编辑器。
  * 绘图应用中的撤销/重做功能。
*   **代码示例**：

    ```swift
    let undoManager = UndoManager()
    var text = "Hello"

    func updateText(to newText: String) {
        let oldText = text
        text = newText
        
        undoManager.registerUndo(withTarget: self) { target in
            target.updateText(to: oldText)
        }
    }

    updateText(to: "Hello, World!")
    print(text)  // 输出: Hello, World!

    undoManager.undo()
    print(text)  // 输出: Hello
    ```

***

#### 2. **State Restoration（状态恢复）**

iOS 的 **状态恢复** 功能允许应用程序在终止或被系统挂起后，恢复到用户离开时的状态。

* **特点**：
  * 通过保存和恢复视图控制器的状态，达到恢复页面状态的效果。
  * 类似备忘录模式中保存和恢复对象状态的设计。
* **使用场景**：
  * 用户返回到应用时，恢复之前的浏览页面。
* **相关方法**：
  * `encodeRestorableState(with:)`：保存状态。
  * `decodeRestorableState(with:)`：恢复状态。

***

#### 3. **Core Data 的快照（Snapshots）**

Core Data 提供了支持对象状态快照的功能，可以看作是备忘录模式的一种实现。

* **特点**：
  * 保存托管对象的当前状态。
  * 可用于实现撤销/重做或数据恢复功能。
* **使用场景**：
  * 在数据模型中进行修改时保存原始状态。
  * 允许用户在提交更改前撤销。
* **相关功能**：
  * `undoManager`：与 Core Data 结合使用时，管理对象的状态变化。

***

#### 4. **UserDefaults**

`UserDefaults` 可以看作是一个轻量级的备忘录工具，适合保存简单的应用状态或用户偏好设置。

* **特点**：
  * 持久化存储小型数据。
  * 保存应用状态以便在重启时恢复。
* **使用场景**：
  * 保存用户的设置，如主题模式、语言选择等。
  * 恢复上一次的使用状态。
*   **代码示例**：

    ```swift
    let defaults = UserDefaults.standard
    defaults.set("Hello, World!", forKey: "SavedText")

    if let savedText = defaults.string(forKey: "SavedText") {
        print(savedText)  // 输出: Hello, World!
    }
    ```

***

#### 5. **NSCoder 和归档机制**

通过 `NSCoder` 和归档机制，iOS 可以保存对象的状态到文件中，并在需要时恢复。

* **特点**：
  * 保存复杂对象的状态快照。
  * 支持深度对象状态存储。
* **使用场景**：
  * 保存用户配置。
  * 恢复复杂对象的状态。
*   **代码示例**：

    ```swift
    class Person: NSObject, NSCoding {
        var name: String
        init(name: String) {
            self.name = name
        }
        
        func encode(with coder: NSCoder) {
            coder.encode(name, forKey: "name")
        }
        
        required init?(coder: NSCoder) {
            name = coder.decodeObject(forKey: "name") as! String
        }
    }

    // 保存对象
    let person = Person(name: "John")
    let data = try! NSKeyedArchiver.archivedData(withRootObject: person, requiringSecureCoding: false)

    // 恢复对象
    let restoredPerson = try! NSKeyedUnarchiver.unarchiveTopLevelObjectWithData(data) as! Person
    print(restoredPerson.name)  // 输出: John
    ```

***

#### 6. **NSUndoManager（macOS 和 iOS）**

macOS 和 iOS 的 `NSUndoManager` 是系统级的撤销/重做工具，非常类似于备忘录模式的实现。

* **特点**：
  * 保存撤销栈和重做栈。
  * 提供简单的方法管理撤销操作。
* **使用场景**：
  * 文本编辑器。
  * 数据编辑工具。

***

#### 7. **UIKit 中的 View 快照**

UIKit 提供了 `snapshotView(afterScreenUpdates:)` 方法，可以捕获当前视图的视觉快照，类似备忘录中保存“当前状态”的概念。

* **特点**：
  * 保存当前 UI 状态的图像快照。
  * 不保存逻辑状态，仅保存外观。
* **使用场景**：
  * 动画效果（如截图并叠加）。
  * 保存界面当前的外观。

***

#### 8. **Photos Framework 的编辑历史**

iOS 的 Photos 框架允许开发者保存和恢复照片编辑历史，类似于备忘录模式中的状态保存和恢复。

* **特点**：
  * 保存编辑操作的状态。
  * 支持回撤到原始状态。
* **使用场景**：
  * 照片编辑器。
  * 视频剪辑工具。

***

#### 总结

iOS 系统中许多工具和框架都内嵌了类似备忘录模式的功能，包括但不限于：

* 撤销/重做管理器（`UndoManager`）
* 数据状态保存（Core Data、UserDefaults、NSCoder）
* 状态恢复（State Restoration）
* UI 快照（视图快照功能）

这些工具为开发者提供了实现撤销/重做、状态保存与恢复的便利，简化了备忘录模式在实际开发中的应用。
