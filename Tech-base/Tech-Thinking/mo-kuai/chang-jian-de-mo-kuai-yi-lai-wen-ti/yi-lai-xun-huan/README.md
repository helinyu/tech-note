# 依赖循环

在 iOS 开发中，**模块的循环依赖**会导致项目结构复杂、编译失败或运行时错误。以下是处理循环依赖的常见方法，结合实际的 iOS 框架和工具：

#### 1. **依赖倒置原则（Dependency Inversion Principle, DIP）**

* **引入协议（Protocol）进行依赖倒置**：将模块间的依赖关系转换为依赖于抽象（即协议）而不是具体的实现。通过定义协议，模块 A 不再直接依赖模块 B 的实现，而是依赖于模块 B 所遵循的协议，从而解耦。
  *   **示例**：

      ```objective-c
      @protocol BProtocol <NSObject>
      - (void)doSomething;
      @end

      @interface A : NSObject
      @property (nonatomic, weak) id<BProtocol> delegate;
      @end
      ```
* 在上面的例子中，A 模块依赖于协议 `BProtocol`，而不是具体的 B 实现，从而避免了 A 和 B 之间的直接依赖。

#### 2. [**依赖注入（Dependency Injection, DI）**](yi-lai-zhu-ru.md)

* **使用依赖注入**来将依赖关系注入到模块内部，而不是由模块自身创建依赖对象。依赖注入可以通过构造函数注入、属性注入或者方法注入来实现。
*   **示例**：

    ```swift
    class ModuleA {
        var moduleB: ModuleB
        
        init(moduleB: ModuleB) {
            self.moduleB = moduleB
        }
    }
    ```

    在这个例子中，`ModuleA` 通过构造函数注入 `ModuleB`，而不是直接依赖 `ModuleB` 的具体实现，从而消除了直接的耦合。

#### 3. **中介者模式（Mediator Pattern）**

* **引入中介者模式**：如果两个模块之间有循环依赖，可以通过引入第三方中介模块来管理模块之间的通信。中介者作为中心点，负责模块间的协调和依赖管理。
* **示例**：
  *   模块 A 和 B 之间依赖，改为两者都依赖中介者 Mediator，模块 A 和模块 B 不再直接依赖彼此，解除了循环依赖。

      ```swift
      class Mediator {
          var moduleA: ModuleA?
          var moduleB: ModuleB?
      }
      ```

#### 4. **使用通知机制（Notification Center）**

* **NSNotificationCenter** 是一种松耦合的模块通信方式。可以通过通知机制解耦两个模块之间的依赖关系。
* **示例**：
  *   模块 A 发送通知，模块 B 订阅该通知并响应，双方不需要直接依赖对方。

      ```swift
      // ModuleA
      NotificationCenter.default.post(name: NSNotification.Name("EventFromA"), object: nil)

      // ModuleB
      NotificationCenter.default.addObserver(self, selector: #selector(handleEvent), name: NSNotification.Name("EventFromA"), object: nil)
      ```

#### 5. **委托模式（Delegate Pattern）**

* **委托模式**允许模块通过代理对象进行通信，而不直接依赖另一模块。通常用于减少模块之间的耦合，避免循环依赖。
* **示例**：
  *   模块 A 通过定义一个代理接口，让模块 B 实现该接口，从而通过代理与 B 交互，而不直接依赖 B 的实现。

      ```swift
      protocol ModuleADelegate: AnyObject {
          func didReceiveData(_ data: String)
      }

      class ModuleA {
          weak var delegate: ModuleADelegate?
          
          func fetchData() {
              delegate?.didReceiveData("some data")
          }
      }

      class ModuleB: ModuleADelegate {
          func didReceiveData(_ data: String) {
              print("Received data: \(data)")
          }
      }
      ```

#### 6. **依赖管理工具和框架**

* 使用依赖管理工具（如 **CocoaPods**、**Swift Package Manager**）在项目中明确第三方库或模块的依赖版本，避免引入不兼容的版本或模块，间接避免了循环依赖问题。

#### 7. **弱引用解决循环依赖**

* 在某些情况下，特别是 **Objective-C** 和 **Swift** 中，强引用可能导致循环依赖。通过使用**弱引用（weak）或无主引用（unowned）**，可以打破引用循环。
*   **示例**：

    ```swift
    class ModuleA {
        weak var moduleB: ModuleB?  // 使用弱引用打破循环
    }
    ```

#### 8. **分层架构**

* 通过设计**分层架构**，确保模块之间的依赖是单向的。常见的分层结构包括：UI 层、服务层、数据层。高层依赖于低层，低层不依赖于高层，确保依赖关系不会形成闭环。
* **示例**：
  * UI 层调用服务层，服务层调用数据层。这样，依赖关系是从上到下的单向依赖，避免循环。

#### 9. **通过模块抽取避免循环依赖**

* 如果两个模块功能耦合度过高，可以考虑将其中的共用逻辑提取出来，作为一个**独立的模块**，让两个模块都依赖该新模块，而不是互相依赖。
* **示例**：
  * 模块 A 和模块 B 都依赖相同的工具方法，可以将工具方法抽取到一个工具模块中。

#### 10. **监控与测试**

* 在项目中使用**依赖图工具**（例如 Xcode 的编译依赖图）来检查模块间的依赖关系。如果发现循环依赖，及时调整模块结构和设计。
* **单元测试**与**集成测试**：通过编写良好的测试用例，确保模块修改不会引入新的循环依赖问题。

#### 总结

处理 iOS 开发中的模块循环依赖，核心思想是通过 **依赖倒置**、**抽象接口**、**依赖注入**、**弱引用** 等方式进行模块间解耦。同时，分层设计、委托模式、中介者模式等设计模式也是有效解决方案。
