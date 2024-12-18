# 中介者 vs 协调者

**中介者模式（Mediator Pattern）** 和 **协调者模式（Coordinator Pattern）** 示例代码，并展示它们的输出。

#### 1. **中介者模式（Mediator Pattern）示例**

在这个示例中，我们将实现一个简单的聊天室，中介者负责协调用户之间的消息传递。

```swift
// Mediator Protocol
protocol Mediator {
    func send(message: String, colleague: Colleague)
}

// ConcreteMediator
class ChatRoom: Mediator {
    var colleagues: [Colleague] = []

    func addColleague(_ colleague: Colleague) {
        colleagues.append(colleague)
        colleague.mediator = self
    }

    func send(message: String, colleague: Colleague) {
        for c in colleagues {
            if c !== colleague {
                c.receive(message)
            }
        }
    }
}

// Colleague Protocol
protocol Colleague {
    var mediator: Mediator? { get set }
    func send(message: String)
    func receive(_ message: String)
}

// ConcreteColleague (User)
class User: Colleague {
    var mediator: Mediator?
    let name: String

    init(name: String) {
        self.name = name
    }

    func send(message: String) {
        mediator?.send(message: message, colleague: self)
    }

    func receive(_ message: String) {
        print("\(name) received: \(message)")
    }
}

// Usage
let chatRoom = ChatRoom()

let user1 = User(name: "Alice")
let user2 = User(name: "Bob")
let user3 = User(name: "Charlie")

chatRoom.addColleague(user1)
chatRoom.addColleague(user2)
chatRoom.addColleague(user3)

user1.send(message: "Hello, everyone!")
user2.send(message: "Hi, Alice!")
```

#### **中介者模式的输出**：

```
Bob received: Hello, everyone!
Charlie received: Hello, everyone!
Alice received: Hi, Alice!
```

在这个代码中，`ChatRoom` 作为中介者，协调不同的用户之间的消息传递。每个用户发送的消息都会被中介者转发给其他用户，而不会直接与其他用户通信。

#### 2. **协调者模式（Coordinator Pattern）示例**

在这个示例中，我们将模拟一个订单处理系统，`OrderCoordinator` 负责协调订单、库存和发货模块。

```swift
// Coordinator Protocol
protocol Coordinator {
    func processOrder(order: Order)
}

// Order class
class Order {
    let id: String
    var isValid: Bool

    init(id: String, isValid: Bool) {
        self.id = id
        self.isValid = isValid
    }
}

// Inventory Manager
class InventoryManager {
    func reserveStock(for order: Order) {
        print("Reserving stock for Order \(order.id)...")
    }
}

// Shipping Manager
class ShippingManager {
    func scheduleShipping(for order: Order) {
        print("Scheduling shipping for Order \(order.id)...")
    }
}

// Alert Manager
class AlertManager {
    func sendAlert(for order: Order) {
        print("Alert: Order \(order.id) is invalid!")
    }
}

// ConcreteCoordinator
class OrderCoordinator: Coordinator {
    let inventoryManager = InventoryManager()
    let shippingManager = ShippingManager()
    let alertManager = AlertManager()

    func processOrder(order: Order) {
        if order.isValid {
            inventoryManager.reserveStock(for: order)
            shippingManager.scheduleShipping(for: order)
        } else {
            alertManager.sendAlert(for: order)
        }
    }
}

// Usage
let order1 = Order(id: "12345", isValid: true)
let order2 = Order(id: "67890", isValid: false)

let coordinator = OrderCoordinator()

coordinator.processOrder(order: order1)
coordinator.processOrder(order: order2)
```

#### **协调者模式的输出**：

```
Reserving stock for Order 12345...
Scheduling shipping for Order 12345...
Alert: Order 67890 is invalid!
```

在这个示例中，`OrderCoordinator` 作为协调者，负责协调订单的处理流程。当订单有效时，协调者会调用库存管理和发货管理模块；如果订单无效，协调者会通知警报模块。

#### 总结：

* **中介者模式** 主要是将通信从直接对象之间转移到中介者对象中，通常不涉及复杂的业务逻辑，主要负责消息的传递。
* **协调者模式** 在协调多个对象的交互时，除了通信协调外，还涉及更多的业务逻辑和调度任务，例如决策、流程控制等。
