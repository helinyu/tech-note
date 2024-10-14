# \_\_covariant协变

在 Objective-C 中，`__covariant` 是一种类型修饰符，允许在泛型中使用协变（covariant）类型。<mark style="color:red;">协变的意思是，如果一个类是另一个类的子类，那么使用子类作为泛型类型参数是允许的</mark>。例如，在 `NSArray` 中，协变使得可以将一个包含子类对象的数组赋值给一个父类对象数组的指针。

举个例子：

```objective-c
NSArray<NSString *> *stringArray = @[@"hello", @"world"];
NSArray<id> *anyObjectArray = stringArray; // 这是合法的，因为 NSArray 是协变的
```

这里的 `NSArray` 是协变的，允许将 `NSArray<NSString *>` 赋值给 `NSArray<id>`。这在许多情况下让代码更具灵活性，因为它可以在不改变 API 的情况下使用更具体的类型。

#### 使用 `__covariant`

在 Objective-C 中，`__covariant` 常用于定义类的泛型类型参数，使得某个泛型类型参数可以接受更具体的类型。这对于创建类型安全的 API 非常有用，尤其是在处理集合类时。

```objective-c
@interface MyContainer<__covariant ObjectType> : NSObject
@property (nonatomic, strong) ObjectType object;
@end
```

这里 `ObjectType` 是协变的，这意味着你可以将 `MyContainer<NSString *>` 类型的对象赋给 `MyContainer<id>` 类型的变量，因为 `NSString` 是 `id` 的子类。

<mark style="color:orange;">协变广泛应用于一些静态强类型语言（如 Swift 和 C#）中，它有助于提高代码的灵活性和类型安全性</mark>。



{% hint style="info" %}
协变允许子类或派生类型的对象在需要父类或基类型的地方使用，从而更灵活地处理类型。
{% endhint %}

