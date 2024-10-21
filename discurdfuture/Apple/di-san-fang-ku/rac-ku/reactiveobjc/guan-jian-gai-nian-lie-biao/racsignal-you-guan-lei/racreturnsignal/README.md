# RACReturnSignal

该Objective-C类`RACReturnSignal`用于创建一个返回单一值的信号。主要功能如下：

1. **初始化与单例**：对于常见的返回值（如`RACUnit.defaultUnit`和`nil`），在发布版本中使用单例优化性能。
2. **订阅处理**：通过`subscribe:`方法，在订阅时立即发送保存的值，并标记完成。
3. **调试信息**：在调试模式下允许自定义信号名称以方便调试。
