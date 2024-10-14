# 协变 vs 逆变



{% hint style="info" %}
逆变和协变都是类型安全产生的概念；

其实就是：

协变：让返回的类型可以是子类型  —— 输出

逆变：让参数可以是父类型 —— 输入
{% endhint %}

```
@interface RACCommand<__contravariant InputType, __covariant ValueType> : NSObject
可以看到这样的定义
```



协变（covariance）和逆变（contravariance）在 Objective-C 泛型中并不十分常见，但它们是理解类型系统中的灵活性和安全性的重要概念。以下是协变和逆变的概念和示例：

#### 协变（Covariance）

协变允许将子类对象赋值给父类泛型对象（从**具体到通用**）。这在返回类型中尤其有用，因为可以向上兼容。例如，如果我们有一个 `RACSignal` 类的子类 `RACSubject`，协变可以让 `RACSignal<NSString *>` 赋值给 `RACSignal<id>`。

```objective-c
@interface RACSignal<__covariant ValueType> : NSObject
@end

RACSignal<NSString *> *stringSignal = [[RACSignal alloc] init];
RACSignal<id> *anySignal = stringSignal; // 合法，因为 RACSignal 是协变的
```

这里，通过使用 `__covariant`，`RACSignal` 能够将 `RACSignal<NSString *>` 赋值给 `RACSignal<id>`，保证类型的灵活性。

#### 逆变（Contravariance）

逆变允许将父类泛型对象赋值给子类泛型对象（从**通用到具体**）。在 Objective-C 中使用 `__contravariant` 让泛型参数接受更广泛的类型，主要用于参数类型。例如：

```objective-c
@interface MyHandler<__contravariant InputType> : NSObject
- (void)handle:(InputType)input;
@end
```

在上面的代码中，`MyHandler` 的泛型参数 `InputType` 使用了 `__contravariant`，因此可以传递更广泛的类型作为参数：

```objective-c
MyHandler<id> *objectHandler = [[MyHandler alloc] init];
MyHandler<NSString *> *stringHandler = objectHandler; // 合法，逆变允许更具体的类型
[stringHandler handle:@"Hello, world!"];
```

这里，逆变使得 `MyHandler<id>` 可以赋值给 `MyHandler<NSString *>`，所以我们能够创建一个接受 `id` 类型的处理器，并将其传递给一个期待 `NSString` 类型的处理器。

#### 总结

* **协变** (`__covariant`)：用于<mark style="color:red;">返回类型</mark>，使子类泛型可以赋值给父类泛型。
* **逆变** (`__contravariant`)：用于<mark style="color:red;">参数类型</mark>，使父类泛型可以赋值给子类泛型。

在实际开发中，协变和逆变让代码更灵活并提高了类型安全性。
