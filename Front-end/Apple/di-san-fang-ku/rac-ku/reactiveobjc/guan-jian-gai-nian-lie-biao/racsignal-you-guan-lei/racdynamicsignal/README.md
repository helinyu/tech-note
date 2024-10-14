# RACDynamicSignal

1. **创建信号**：`+createSignal:`方法通过拷贝传入的block到`_didSubscribe`属性，并设置信号名称后返回一个信号对象。
2. **管理订阅者**：`-subscribe:`方法用于添加订阅者，通过`RACCompoundDisposable`管理多个可释放资源。当有订阅者时，会调度执行`_didSubscribe`中的block并将结果加入管理器。
