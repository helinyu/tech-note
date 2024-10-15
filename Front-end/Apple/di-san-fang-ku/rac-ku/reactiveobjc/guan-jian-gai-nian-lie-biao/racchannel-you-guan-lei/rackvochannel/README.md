# RACKVOChannel

继承[RACChannel](../racchannel/)

该头文件定义了 `RACChannelTo` 宏和 `RACKVOChannel` 类，<mark style="color:red;">**用于创建观察对象属性变化的通道**</mark>。主要功能如下：

1. **宏 `RACChannelTo`**：创建一个 `RACKVOChannel` 实例，观察指定对象的键路径（`keyPath`）属性变化。当目标对象被销毁时，通道完成。
2. **类 `RACKVOChannel`**：
   * 初始化方法 `-initWithTarget:keyPath:nilValue:`：初始化一个观察特定对象和键路径的通道。
   * 当目标对象释放时，通道完成。
   * 支持发送当前值及未来的变化给订阅者，并能设置 `nil` 值时的默认值。
3. **辅助方法**：提供用于宏操作的方法，如 `objectForKeyedSubscript:` 和 `setObject:forKeyedSubscript:`。

用于观察并同步对象的键值路径变化。主要功能包括：

1. **初始化**：通过`initWithTarget:target keyPath:keyPath nilValue:nilValue`方法初始化，设置目标对象和键值路径，并开始观察目标对象的变化。
2. **线程局部数据管理**：通过`RACKVOChannelData`类管理线程局部数据，用于标记是否忽略下一次更新。
3. **观察与同步**：观察目标对象的键值路径变化，并将变化同步到终端（terminal）。同时，更新目标对象时会设置标志以避免循环触发。
4. **错误处理**：在同步过程中遇到错误时进行断言检查和日志记录。
5. **对象释放处理**：当目标对象被释放时，停止观察并完成通道。
6. **子脚本设置**：实现了键值脚本相关的方法，用于设置或获取子脚本对象。







