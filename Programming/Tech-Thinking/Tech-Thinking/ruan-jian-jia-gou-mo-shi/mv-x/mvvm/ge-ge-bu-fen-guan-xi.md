# 各个部分关系

以下是MVVM（Model-View-ViewModel）各个部分之间关系的简要图示：

```
          +---------------+
          |    Model      |
          +---------------+
                 ↑
                 |  (data binding)
                 |
          +---------------+
          |  ViewModel    |
          +---------------+
                 ↑
          (commands / data binding)
                 |
                 ↓
          +---------------+
          |     View      |
          +---------------+
```

#### 关系描述

1. **Model**：
   * 负责业务逻辑和数据管理。
   * ViewModel通过直接引用Model来获取和更新数据。
2. **ViewModel**：
   * 作为Model和View之间的中介，处理来自View的用户输入，并调用Model进行数据操作。
   * 通过数据绑定将Model的数据传递给View，确保View能反映最新的数据状态。
   * 处理用户命令（如按钮点击等），并更新Model。
3. **View**：
   * 显示用户界面，呈现从ViewModel获取的数据。
   * 通过数据绑定接收来自ViewModel的数据更新，以及向ViewModel发送用户交互事件。

#### 数据流

* **单向数据流**：在典型的MVVM实现中，数据流通常是单向的，即从Model到ViewModel再到View。用户的输入通过View传递到ViewModel，ViewModel进行处理后可能会更新Model。
* **双向数据绑定**：在一些框架（如Angular、React或SwiftUI）中，MVVM还支持双向数据绑定，使得Model的变化能够自动反映到View上，反之亦然。、

