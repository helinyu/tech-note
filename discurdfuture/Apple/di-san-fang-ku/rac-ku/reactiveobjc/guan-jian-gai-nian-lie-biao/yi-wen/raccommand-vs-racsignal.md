# RACCommand vs RACSignal

`RACCommand` 和 `RACSignal` 是 ReactiveObjC 中密切相关的两个类，它们的关系主要体现在 **动作封装** 和 **信号管理** 上。`RACCommand` 是一个专门设计用于封装“动作”或“事件”的类，而 `RACSignal` 是一个用于传递数据流的核心类。`RACCommand` 使用 `RACSignal` 来实现其事件的处理和响应。

#### `RACCommand` 和 `RACSignal` 的关系

1. **`RACCommand` 通过 `RACSignal` 表示每次执行的结果**：
   * 每次执行 `RACCommand` 时，`RACCommand` 会创建一个 `RACSignal`，该信号表示执行的过程和结果。
   * 当我们在初始化 `RACCommand` 时，传入的 `signalBlock` 就是一个返回 `RACSignal` 的闭包，它会被 `RACCommand` 在每次执行时调用并返回一个新的 `RACSignal`。
2. **`executionSignals` 属性管理所有的执行信号**：
   * `RACCommand` 的 `executionSignals` 是一个信号的信号（即 `RACSignal<RACSignal *>`），用于发出每次执行 `RACCommand` 时产生的 `RACSignal`。
   * 可以通过 `executionSignals` 订阅每次执行的信号流，并通过 `switchToLatest` 获取最新的执行信号，这样就能对每次执行的结果进行处理。
3. **`enabled` 和 `executing` 信号的辅助控制**：
   * `enabled` 信号控制 `RACCommand` 是否可以执行，它通常是一个 `RACSignal`，表明当前状态是否允许执行（比如按钮是否可以点击）。
   * `executing` 信号则用于表示当前 `RACCommand` 的执行状态。这个信号在执行中时发出 `YES`，完成后发出 `NO`。通过这个信号，可以在操作执行时显示加载指示器等 UI 变化。
4. **`errors` 信号用于传递执行过程中的错误**：
   * 如果 `RACCommand` 的执行过程产生错误，错误会被捕获到 `errors` 信号中，方便统一的错误处理。

#### `RACCommand` 和 `RACSignal` 的使用示例

例如，我们可以将一个按钮点击事件封装成 `RACCommand` 并监听结果：

```objc
// 初始化 RACCommand，signalBlock 返回一个 RACSignal
self.loginCommand = [[RACCommand alloc] initWithSignalBlock:^RACSignal *(id input) {
    // 返回表示登录请求的信号
    return [self loginSignal];
}];

// 监听执行结果
[self.loginCommand.executionSignals.switchToLatest subscribeNext:^(id result) {
    NSLog(@"登录成功：%@", result);
}];

// 监听执行中的错误
[self.loginCommand.errors subscribeNext:^(NSError *error) {
    NSLog(@"登录失败：%@", error);
}];

// 设置按钮的点击事件
self.loginButton.rac_command = self.loginCommand;
```

#### 代码解析

* `initWithSignalBlock:`：每次执行 `loginCommand` 时都会调用 `signalBlock`，并返回一个 `RACSignal`。
* `executionSignals.switchToLatest`：通过 `switchToLatest` 可以获取到每次最新的执行信号，监听登录结果。
* `errors`：如果 `loginSignal` 执行过程中产生错误，它会被捕获到 `errors` 信号，进行统一错误处理。

#### 总结

* **`RACCommand` 是动作的封装，而 `RACSignal` 是数据的载体**。
* **每次执行 `RACCommand`，都会创建并返回一个 `RACSignal` 表示执行过程和结果**。
* **`RACCommand` 利用 `executionSignals` 管理执行信号，并通过 `errors` 信号来管理错误**。

这种关系让 `RACCommand` 能够以响应式编程的方式管理动作和状态，使得事件的执行逻辑和数据流的处理更加清晰和解耦。
