# 逆变

`__contravariant` 是 Objective-C 中的一种类型修饰符，用于泛型类型参数。它表示_逆变_（contravariance）关系，即允许泛型参数使用更**通用**的类型。

#### 逆变的概念

逆变（contravariance）允许将一个类型的子类泛型容器赋值给一个父类泛型容器。例如，逆变在参数类型中允许_更广泛_的类型。**与协变（covariance）相反**，协变允许泛型容器使用更**具体**的类型。

#### 逆变的作用

在 Objective-C 中使用 `__contravariant` 时，可以让泛型参数接受更广泛的类型，通常在协议或者方法参数中使用，以便让泛型类型更加通用。

#### 举例

例如，假设我们有一个泛型接口或协议，其泛型参数声明为逆变：

```objective-c
@interface MyClass<__contravariant ObjectType> : NSObject
- (void)doSomething:(ObjectType)object;
@end
```

在这个例子中，由于 `ObjectType` 是逆变的，所以在调用 `doSomething:` 时，传入的对象类型可以是 `ObjectType` 的父类型。

#### 逆变的应用场景

* **参数类型**：允许在参数类型中使用更加宽泛的类型。
* **灵活性**：在一些需要接受父类或更通用类型的场景下使用，有助于代码的复用和扩展。

总结来说，`__contravariant` 使泛型参数能够向更宽泛的父类方向兼容，主要用于参数类型的泛型设计。
