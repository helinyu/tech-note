# 数据流方向



{% hint style="info" %}
数据流的方向： 单向数据流 、 双向数据流

思考，走过去是否有回来的过程。
{% endhint %}

在 MVC、MVP 和 MVVM 架构中，数据流方向的特点如下：

1. **MVC（Model-View-Controller）**：双向数据流
   * **View → Controller**：用户与 View 交互，事件传递给 Controller。
   * **Controller → Model**：Controller 根据用户操作更新 Model 数据。
   * **Model → View**：Model 数据改变后，通知 View 更新界面。
   * **特点**：数据从 View 流向 Controller，再更新 Model，然后反向通知 View。
2. **MVP（Model-View-Presenter）**：双向数据流
   * **View → Presenter**：View 将用户输入传递给 Presenter。
   * **Presenter → Model**：Presenter 调用 Model，获取或更改数据。
   * **Model → Presenter → View**：Model 数据变化后，Presenter 更新 View。
   * **特点**：Presenter 负责协调 View 和 Model 之间的交互，数据在三者间双向流动。
3. **MVVM（Model-View-ViewModel）**：主要是双向数据流
   * **View ↔ ViewModel**：双向绑定，View 和 ViewModel 数据自动同步。
   * **ViewModel → Model**：ViewModel 从 Model 获取数据或保存用户输入。
   * **特点**：View 和 ViewModel 通过双向绑定保持同步，ViewModel 处理数据和业务逻辑，通常只有 ViewModel 主动访问 Model，不直接向 View 反馈。

在**MVVM**中，数据流向更清晰，特别适合数据频繁更新的应用，而**MVP 和 MVC** 因为更灵活，适合需求变动多的中小型应用。
