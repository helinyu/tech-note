# iOS中的消息发送机制和消息转发机制的区别

iOS中的消息发送机制和消息转发机制是 Objective-C 语言中重要的特性，分别用于处理方法调用和响应的机制。它们的区别如下：

#### 消息发送机制

1. **基本概念**：当你调用一个对象的方法时，实际上是向该对象发送了一条消息。
2. **查找方法**：在发送消息时，运行时会首先查找对象的类及其父类中是否实现了该方法。
3. **效率**：如果找到相应的方法，直接调用该方法；如果没有找到，则会抛出异常。
4. **快速响应**：大部分消息发送是直接的，效率较高。

#### 消息转发机制

1. **基本概念**：当对象无法处理某条消息时，会触发消息转发机制。
2. **转发流程**：
   * **动态解析**：首先调用 `+resolveInstanceMethod:` 或 `+resolveClassMethod:`，允许对象动态添加方法实现。
   * **消息转发**：如果没有处理，运行时会调用 `-forwardingTargetForSelector:`，可返回另一个对象来处理该消息。
   * **完全转发**：如果仍未找到处理方式，则会调用 `-methodSignatureForSelector:` 和 `-forwardInvocation:`，允许开发者手动处理未响应的消息。
3. **灵活性**：消息转发机制提供了更大的灵活性，允许你在运行时改变对象的行为。

#### 总结

* 消息发送机制是一个直接和高效的过程，主要用于对象能够响应的情况。
* 消息转发机制用于处理无法响应的消息，通过一系列方法允许动态处理，提供了更大的灵活性。