# RACGroupedSignal

继承 [RACSubject](../racsubject/)

1. **扩展信号类**：继承自某个未展示的基础类，用于处理分组信号。
2. **添加键属性**：实例变量 `key` 用于存储信号的分组键。
3. **创建分组信号**：`+signalWithKey:` 方法创建一个带有指定键的 `RACGroupedSignal` 实例，并返回它。

简而言之，这个类主要用于根据键值对信号进行分组处理。



