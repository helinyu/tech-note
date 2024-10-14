# OC中泛型继承以及协议

```
@interface RACSubject<ValueType> : RACSignal<ValueType> <RACSubscriber>

/// Returns a new subject.
+ (instancetype)subject;

// Redeclaration of the RACSubscriber method. Made in order to specify a generic type.
- (void)sendNext:(nullable ValueType)value;

@end

```

在 `Objective-C` 中，`<ValueType>` 和 `<RACSubscriber>` 的含义和用法不同，它们分别代表**泛型类型参数**和**协议**。

#### `<ValueType>` - 泛型类型参数

`<ValueType>` 是一种泛型类型参数，它允许 `RACSubject` 指定一个类型，用于在信号传递过程中确保类型安全。通过泛型，`RACSubject` 可以保证它发送和接收的值是符合 `ValueType` 类型的。

例如，`RACSubject<NSString *> *subject` 表示这个 `RACSubject` 只能处理 `NSString` 类型的数据。泛型在编译时生效，提供类型检查和代码提示，减少类型错误。

#### `<RACSubscriber>` - 协议

`<RACSubscriber>` 表示 `RACSubject` 遵循 `RACSubscriber` 协议。协议在 Objective-C 中类似接口，规定了必须实现的一组方法。通过遵循协议，`RACSubject` 类能够充当 `RACSubscriber` 的角色，接收其他信号的数据。

在 `@interface RACSubject<ValueType> : RACSignal<ValueType> <RACSubscriber>` 中，`RACSubject` 是 `RACSignal` 的子类，并且还遵循了 `RACSubscriber` 协议。这样一来，`RACSubject` 可以既作为信号的发送者（符合 `RACSignal`），又可以作为信号的订阅者（符合 `RACSubscriber`），在响应式编程的场景中非常实用。

#### 总结

* **`<ValueType>`**：用于指定 `RACSubject` 传递的数据类型，提供类型安全。
* **`<RACSubscriber>`**：指定 `RACSubject` 遵循 `RACSubscriber` 协议，使其可以作为一个订阅者。
