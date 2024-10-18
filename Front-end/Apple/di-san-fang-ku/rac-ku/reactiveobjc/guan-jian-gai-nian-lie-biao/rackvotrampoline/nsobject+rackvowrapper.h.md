# NSObject+RACKVOWrapper.h

这个方法调用了KVO方法



### 1、头文件方法

{% code overflow="wrap" %}
```cpp
- (RACDisposable *)rac_observeKeyPath:(NSString *)keyPath options:(NSKeyValueObservingOptions)options observer:(__weak NSObject *)observer block:(void (^)(id value, NSDictionary *change, BOOL causedByDealloc, BOOL affectedOnlyLastComponent))block;
```
{% endcode %}

**简略说明：**

1. **开始**：调用 `rac_observeKeyPath:options:observer:block:` 方法。
2. **调用 rac\_observeKeyPath 方法**：
   * 验证传入的参数是否有效。
   * 如果参数有效，继续执行；否则，抛出异常。
3. **创建 RACDisposable 对象**：创建一个 `RACDisposable` 对象，用于管理观察者的生命周期。
4. **设置观察者块**：设置一个块，当指定的键路径发生变化时调用该块。
5. **处理弱引用属性的通知**：处理弱引用属性的自动通知，确保在观察者或被观察对象释放时自动移除观察。
6. **返回 RACDisposable 对象**：返回 `RACDisposable` 对象，可以用来停止观察。

<figure><img src="../../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
