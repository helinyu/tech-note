# 数据流

在 MVP（Model-View-Presenter）架构中，数据流的核心在于<mark style="color:red;">将业务逻辑与界面层解耦</mark>，以实现更好的模块化、可维护性和可测试性。以下是 MVP 的基本数据流：

#### 1. View（视图）

View 层主要负责显示 UI，用户通过 View 进行交互。View 不直接处理数据逻辑，而是将用户操作传递给 Presenter，并在 Presenter 回调数据后更新显示。View 通过接口与 Presenter 交互，从而实现解耦。

#### 2. Presenter（表示层）

Presenter 是数据流的核心，它接收来自 View 的操作请求，并与 Model 进行交互。Presenter 负责处理业务逻辑和数据请求，决定何时向 View 发送数据更新指令。Presenter 和 View 通过接口相互通信，从而实现数据流的控制和更新。

#### 3. Model（模型层）

Model 是数据的来源，可以是本地数据库、远程 API 或缓存等。Model 负责处理数据操作和网络请求等，将数据提供给 Presenter，并通过回调的方式通知 Presenter 数据是否准备好。Presenter 接收 Model 的数据后，再传递给 View。

#### 数据流示例

1. **用户触发操作**：用户在 View 上的操作（如点击按钮）触发事件。
2. **View 将事件传递给 Presenter**：View 通过接口将用户操作传递给 Presenter。
3. **Presenter 请求 Model 获取数据**：Presenter 接收 View 的操作请求后，决定从 Model 请求数据。
4. **Model 返回数据给 Presenter**：Model 完成数据请求后，将数据返回给 Presenter。
5. **Presenter 更新 View**：Presenter 接收数据后，决定如何更新 UI，将数据传递给 View。
6. **View 显示数据**：View 最终根据 Presenter 提供的数据刷新界面。

在 MVP 中，数据流的关键是 View、Presenter、Model 之间的职责分离。这样，业务逻辑集中在 Presenter 中，View 只负责展示，Model 负责数据，使得代码更加易读、易测且易维护。
