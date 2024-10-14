# RACErrorSignal

该Objective-C类`RACErrorSignal`用于创建一个立即发送错误信号的对象。主要功能如下：

1. **初始化错误信号**：通过`+error:`方法创建`RACErrorSignal`实例，并设置待发送的错误。
2. **订阅并发送错误**：通过`-subscribe:`方法订阅信号，并在订阅时立即发送初始化时设置的错误给订阅者。
