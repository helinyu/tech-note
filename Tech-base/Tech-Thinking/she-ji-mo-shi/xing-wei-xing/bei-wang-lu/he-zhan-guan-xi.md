# 和栈关系

**备忘录模式**并不强制使用特定的数据结构来实现，它的实现方式取决于具体需求。然而，在实现中，**栈**常常是备忘录模式的一个合适选择，特别是在需要实现“撤销/重做”功能的场景中。这是因为栈的 **后进先出（LIFO）** 特性非常适合管理状态的存储和恢复。

#### 为什么栈适合备忘录模式？

1. **撤销功能：**
   * 每当保存一个状态时，将其压入栈顶。
   * 当需要撤销操作时，从栈顶弹出最新的状态，恢复到上一个状态。
2. **重做功能（需要双栈）：**
   * 在撤销时，将状态从一个栈弹出并压入另一个栈。
   * 在重做时，从第二个栈弹出状态并恢复，同时重新压入第一个栈。

***

#### 使用栈实现备忘录模式示例

以下是一个简化的示例，展示如何利用栈实现撤销和重做功能：

**Java 示例**

```java
import java.util.Stack;

// 备忘录类
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// 发起人类
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
        System.out.println("State set to: " + state);
    }

    public String getState() {
        return state;
    }

    // 创建备忘录
    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    // 从备忘录恢复状态
    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
        System.out.println("State restored to: " + state);
    }
}

// 管理者类
class Caretaker {
    private Stack<Memento> undoStack = new Stack<>();
    private Stack<Memento> redoStack = new Stack<>();

    public void saveState(Memento memento) {
        undoStack.push(memento);
        redoStack.clear(); // 每次保存新状态时清空重做栈
    }

    public Memento undo() {
        if (!undoStack.isEmpty()) {
            Memento memento = undoStack.pop();
            redoStack.push(memento);
            return memento;
        }
        return null;
    }

    public Memento redo() {
        if (!redoStack.isEmpty()) {
            Memento memento = redoStack.pop();
            undoStack.push(memento);
            return memento;
        }
        return null;
    }
}

// 测试类
public class MementoWithStack {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State #1");
        caretaker.saveState(originator.saveStateToMemento());

        originator.setState("State #2");
        caretaker.saveState(originator.saveStateToMemento());

        originator.setState("State #3");
        caretaker.saveState(originator.saveStateToMemento());

        // 撤销操作
        originator.getStateFromMemento(caretaker.undo()); // 回到 State #2
        originator.getStateFromMemento(caretaker.undo()); // 回到 State #1

        // 重做操作
        originator.getStateFromMemento(caretaker.redo()); // 回到 State #2
    }
}
```

***

#### 栈的优点与适用场景

* **优点：**
  * 管理简单：栈操作只需 `push` 和 `pop`，实现简单直观。
  * 性能高效：操作时间复杂度为 (O(1))。
* **适用场景：**
  * 多步撤销与重做操作。
  * 需要按照状态存储顺序逐步回退。

***

#### 非栈实现的情况

虽然栈常用于备忘录模式，但并不是唯一的选择。以下场景可能使用其他数据结构：

1. **多状态历史管理：**\
   如果需要随机访问某个历史状态，可以使用 **列表** 或 **队列**。
2. **状态持久化：**\
   如果需要将状态长期保存，可以使用 **数据库** 或 **文件系统**。

***

总结：在实现备忘录模式时，是否使用栈取决于功能需求。如果需要实现撤销和重做，栈是一个非常自然的选择。
