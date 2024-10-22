# autorelease对象在什么时机会被调用release

`autorelease` 对象的释放时机依赖于自动释放池（`@autoreleasepool`）的管理机制。具体来说，`autorelease` 方法会将对象添加到当前的自动释放池中，该对象的 `release` 操作会在以下情况下被调用：

#### 1. 自动释放池的作用域结束

当你使用 `@autoreleasepool` 创建一个自动释放池时，在池的作用域结束时，池中的所有对象会被释放。具体流程如下：

```objc
@autoreleasepool {
    // 创建对象并调用 autorelease
    NSObject *obj = [[NSObject alloc] init];
    [obj autorelease]; // 将 obj 添加到自动释放池
} // 这里自动释放池的作用域结束
```

在作用域结束时，自动释放池会遍历其中的所有对象，调用它们的 `release` 方法。

#### 2. 当前事件循环结束

在没有使用 `@autoreleasepool` 的情况下，自动释放的对象会在当前事件循环结束时被释放。这通常适用于 Cocoa 和 Cocoa Touch 的事件驱动模型，系统会在处理完当前事件后清空自动释放池。

#### 3. 嵌套自动释放池

可以在 `@autoreleasepool` 中嵌套多个自动释放池。每个池的释放时机与其作用域有关，内层池的作用域结束时会立即释放其中的对象，外层池的作用域结束时会释放外层池中的对象。

#### 总结

使用 `autorelease` 添加到自动释放池的对象会在自动释放池的作用域结束时调用 `release`，从而释放内存。这种机制帮助开发者管理临时对象的生命周期，避免手动释放带来的复杂性。
