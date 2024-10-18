# 数据流方向

MVP (Model-View-Presenter) 通常也是<mark style="color:red;">**双向数据流**</mark>。其数据流关系如下：

* **View** 和 **Presenter**：View 接收用户输入后将事件传递给 Presenter，Presenter 再调用 Model 进行数据处理，并将结果返回给 View，以便更新界面。
* **Presenter** 和 **Model**：Presenter 直接与 Model 交互，当 Model 数据发生变化时，Presenter 会获取新数据并通过逻辑处理后通知 View 进行更新。

由于 Presenter 位于 View 和 Model 之间，MVP 模式下数据在 Model、View、Presenter 三者之间呈现出一种双向流动的特征。这种架构在一定程度上分离了视图和业务逻辑，便于测试和维护。
