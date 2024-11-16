# 备忘录

**备忘录设计模式**（Memento Design Pattern）是一种行为型设计模式，用于保存对象的状态，以便在以后可以恢复到该状态。它的主要目的是在不破坏对象封装的前提下，捕获和保存对象的内部状态，供后续需要时恢复。

#### 备忘录模式的主要组成部分

1. **Originator（发起人）：**
   * 保存自身状态到备忘录中。
   * 从备忘录中恢复状态。
2. **Memento（备忘录）：**
   * 存储发起人的内部状态。
   * 防止发起人以外的其他对象访问备忘录，确保备忘录的封装性。
3. **Caretaker（管理者）：**
   * 负责保存和恢复备忘录。
   * 不会修改或操作备忘录的内容，只是保存备忘录的引用。![](<../../../.gitbook/assets/image (8).png>)

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

***



#### 实现示例（以文本编辑器为例）

```java
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
    }
}

// 管理者类
class Caretaker {
    private List<Memento> mementoList = new ArrayList<>();

    public void add(Memento state) {
        mementoList.add(state);
    }

    public Memento get(int index) {
        return mementoList.get(index);
    }
}

// 测试类
public class MementoPatternDemo {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State #1");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #2");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #3");

        System.out.println("Current State: " + originator.getState());
        originator.getStateFromMemento(caretaker.get(0));
        System.out.println("First saved State: " + originator.getState());
        originator.getStateFromMemento(caretaker.get(1));
        System.out.println("Second saved State: " + originator.getState());
    }
}
```

***

#### 应用场景

1. **需要保存和恢复对象的状态时**：如文本编辑器的撤销功能。
2. **需要实现事务操作时**：如数据库的回滚操作。
3. **避免过多的数据库存储**：在应用中频繁保存对象状态。

***

#### 优缺点

**优点：**

1. **封装性强：**\
   备忘录将对象的状态封装起来，外界无法直接访问它的内容。
2. **易于恢复：**\
   可以轻松恢复对象的历史状态。

**缺点：**

1. **占用资源：**\
   如果需要存储的状态很多，会占用大量内存。
2. **复杂性增加：**\
   需要引入额外的类（备忘录、管理者）。



<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

备忘录模式常用于开发需要“后悔药”功能的应用，如撤销、回滚等功能，是一种设计优雅且实用的模式。
