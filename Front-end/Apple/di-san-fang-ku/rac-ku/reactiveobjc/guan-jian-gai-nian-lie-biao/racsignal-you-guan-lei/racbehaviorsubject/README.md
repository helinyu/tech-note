# RACBehaviorSubject

1. `+ (instancetype)behaviorSubjectWithDefaultValue:(id)value`：创建一个带有默认值的行为主题实例。
2. `- (RACDisposable *)subscribe:(id<RACSubscriber>)subscriber`：订阅者注册时，立即发送当前值给订阅者，并返回可取消订阅的对象。
3. `- (void)sendNext:(id)value`：更新当前值，并通知所有订阅者。所有操作在同步块中执行以保证线程安全。
