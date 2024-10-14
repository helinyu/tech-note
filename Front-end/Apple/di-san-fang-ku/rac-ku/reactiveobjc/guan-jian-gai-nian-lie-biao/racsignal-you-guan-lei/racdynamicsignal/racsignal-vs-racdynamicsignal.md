# RACSignal vs RACDynamicSignal

<mark style="color:red;">**`其实`**</mark><mark style="color:red;">**RACSignal 没有被实例化，相当于抽象类或者接口，而是通过RACDynamicSignal来实现的。**</mark>



`RACSignal` 和 `RACDynamicSignal` 都是 ReactiveCocoa 中用于处理异步事件流的信号类型，但它们在设计和使用上有一些显著的关系和区别。

#### 关系

1. **`RACDynamicSignal` 是 `RACSignal` 的实现细节**：
   * `RACDynamicSignal` 是通过 `RACSignal` 的 `createSignal:` 方法创建的信号类型。实际上，任何通过 `createSignal:` 创建的信号都会是一个 `RACDynamicSignal` 实例。
   * `RACSignal` 是一个更高级的接口，用户通过它创建和使用信号，而具体的实现细节可能包括 `RACDynamicSignal`。
2. **信号类型的继承**：
   * `RACDynamicSignal` 是 `RACSignal` 的一种特殊实现。它提供了动态生成信号的能力，用户在使用 `createSignal:` 时实际上是在使用 `RACDynamicSignal`。

#### 区别

1. **设计目的**：
   * **`RACSignal`**：是 ReactiveCocoa 中信号的主要抽象，提供了丰富的 API 来创建和操作信号流。它被设计为一个通用的接口，适用于多种异步编程场景。
   * **`RACDynamicSignal`**：主要用于实现动态信号，通过用户自定义的逻辑来决定信号的行为。它不是一个用户直接使用的接口，而是为信号的灵活构建提供支持。
2. **用户接口**：
   * **`RACSignal`**：用户可以直接通过 `RACSignal` 创建信号，例如使用 `createSignal:`、`return:`、`error:`、`interval:` 等静态方法。
   * **`RACDynamicSignal`**：通常不直接创建或使用，开发者主要通过 `RACSignal` 的 API 来使用它。
3. **灵活性与控制**：
   * **`RACSignal`**：提供了广泛的操作符，如 `map`、`filter`、`merge`、`concat` 等，可以用于对信号流进行各种变换和组合。
   * **`RACDynamicSignal`**：允许用户自定义信号的行为和事件的发送时机，适合用于需要动态控制信号流的场景。

#### 代码示例

以下是一个示例，展示了如何通过 `RACSignal` 创建 `RACDynamicSignal`。

```objc
// 使用 RACSignal 创建动态信号
RACSignal *dynamicSignal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    // 发送事件
    [subscriber sendNext:@"Dynamic signal event"];
    [subscriber sendCompleted];
    
    return [RACDisposable disposableWithBlock:^{
        NSLog(@"Dynamic signal disposed");
    }];
}];

// 订阅动态信号
[dynamicSignal subscribeNext:^(id x) {
    NSLog(@"Received: %@", x);
}];
```

在这个例子中，`dynamicSignal` 实际上是一个 `RACDynamicSignal` 的实例，但用户通过 `RACSignal` 的接口进行操作。

#### 总结

* `RACSignal` 是一个高级的、用户友好的接口，用于创建和操作异步事件流。
* `RACDynamicSignal` 是 `RACSignal` 的具体实现，允许动态地定义信号的行为，但一般不直接由用户操作。
* 使用 `RACSignal` 提供的 API，用户可以方便地创建 `RACDynamicSignal`，从而在信号流中实现动态和灵活的行为。
