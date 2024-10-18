# NSObject+RACKVOWrapper.m

代码实现

这段Objective-C代码是`ReactiveObjC`库的一部分，实现了对`NSObject`类的扩展，提供了一个名为`rac_observeKeyPath:`的方法，用于观察对象的键路径变化。主要功能包括：

1. **参数校验**：确保传入的块（block）不为nil，并且键路径至少有一个组件。
2. **初始化资源**：创建必要的可释放对象（`RACCompoundDisposable`、`RACSerialDisposable`等），用于管理观察者的生命周期。
3. **属性检查**：检查目标对象的属性类型，决定是否需要在属性值被释放时触发回调。
4. **添加释放观察者**：为属性值的释放添加回调，确保在值被释放时调用指定的块。
5. **添加键路径观察者**：递归地为键路径的每个组件添加观察者，确保在值变化时调用指定的块。
6. **初始值处理**：如果指定了`NSKeyValueObservingOptionInitial`选项，则在观察开始时立即调用块。
7.  **资源管理**：确保在观察者或目标对象被释放时，所有资源都被正确释放。



    \
    ![](<../../../../../.gitbook/assets/image (2).png>)





1. **开始**：方法开始执行。
2. **参数校验**：检查传入的块和键路径是否有效。
3. **初始化资源**：创建必要的可释放对象，用于管理观察者的生命周期。
4. **属性检查**：检查目标对象的属性类型，决定是否需要在属性值被释放时触发回调。
5. **需要释放观察者?**：根据属性类型决定是否需要添加释放观察者。
6. **添加释放观察者**：为属性值的释放添加回调。
7. **跳过释放观察者**：如果不需要添加释放观察者，则跳过此步骤。
8. **添加键路径观察者**：递归地为键路径的每个组件添加观察者。
9. **有初始值?**：检查是否需要处理初始值。
10. **处理初始值**：如果指定了`NSKeyValueObservingOptionInitial`选项，则在观察开始时立即调用块。
11. **跳过初始值处理**：如果不需要处理初始值，则跳过此步骤。
12. **管理资源**：确保在观察者或目标对象被释放时，所有资源都被正确释放。
13. **返回可释放对象**：返回一个可释放对象，用于手动停止观察。\


***

相比系统自带的KVO，ReactiveObjC的`RACKVOWrapper`主要增加了以下几点功能和改进：

1. **资源管理**：
   * **自动清理**：使用`RACDisposable`和`RACCompoundDisposable`来管理观察者的生命周期，确保在对象释放时自动清理资源，避免内存泄漏。
   * **复合Disposable**：通过`RACCompoundDisposable`和`RACSerialDisposable`来管理多个Disposable对象，方便统一管理和释放。
2. **增强的错误处理**：
   * **参数校验**：在方法开始时对传入的参数进行校验，确保block和keyPath的有效性，提高代码的健壮性。
3. **灵活的回调机制**：
   * **初始值处理**：支持在观察开始时立即调用block处理初始值，通过`NSKeyValueObservingOptionInitial`选项控制。
   * **优先通知**：支持在值变化前调用block，通过`NSKeyValueObservingOptionPrior`选项控制。
4. **属性类型检查**：
   * **属性检查**：检查目标对象的属性类型，确定是否需要添加dealloc观察者，避免不必要的观察和潜在的错误。
5. **嵌套键路径支持**：
   * **多级键路径**：支持多级键路径的观察，通过递归调用`rac_observeKeyPath`方法，处理嵌套的键路径变化。
6. **线程安全**：
   * **并发处理**：在处理键路径变化时，使用`RACSerialDisposable`来确保线程安全，避免并发问题。

#### 具体实现细节

1. **资源管理**：
   * 使用`RACCompoundDisposable`来管理多个Disposable对象，确保在对象释放时自动清理所有资源。
   * 使用`RACSerialDisposable`来管理单个Disposable对象，确保在并发情况下正确处理资源。
2. **增强的错误处理**：
   * 在方法开始时使用`NSCParameterAssert`对传入的参数进行校验，确保block和keyPath的有效性。
3. **灵活的回调机制**：
   * 支持`NSKeyValueObservingOptionInitial`选项，可以在观察开始时立即调用block处理初始值。
   * 支持`NSKeyValueObservingOptionPrior`选项，可以在值变化前调用block。
4. **属性类型检查**：
   * 使用`class_getProperty`和`rac_copyPropertyAttributes`来获取属性的类型信息，判断是否需要添加dealloc观察者。
5. **嵌套键路径支持**：
   * 通过递归调用`rac_observeKeyPath`方法，处理多级键路径的变化。
6. **线程安全**：
   * 使用`RACSerialDisposable`来确保在并发情况下正确处理资源，避免并发问题。

这些改进使得`RACKVOWrapper`在使用KVO时更加安全、灵活和高效。



