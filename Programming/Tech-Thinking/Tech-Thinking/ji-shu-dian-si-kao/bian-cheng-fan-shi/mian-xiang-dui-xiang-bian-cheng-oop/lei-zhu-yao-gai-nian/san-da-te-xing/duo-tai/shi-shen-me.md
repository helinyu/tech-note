# 是什么？

多态（Polymorphism）是面向对象编程中的一个核心概念，它允许一个接口有多种不同的实现。简单来说，<mark style="color:red;">**多态使得同一个函数或方法可以根据传递的对象类型表现出不同的行为**</mark>。它提高了代码的<mark style="color:orange;">灵活性和可扩展性。</mark>

多态有两种常见形式：

1. **编译时多态（静态多态）**：
   * 通过<mark style="color:red;">方法重载（Method Overloading）或运算符重载（Operator Overloading）</mark>来实现。
   * 编译器在编译时决定调用哪一个方法或运算符实现。
   * 例如在C++中，可以定义多个具有相同名字但参数不同的函数，编译器会根据参数的不同来选择具体调用哪个函数。
2. **运行时多态（动态多态）**：
   * 通过<mark style="color:red;">继承和方法重写（Method Overriding）</mark>来实现。
   * 在运行时决定调用哪个具体的方法。
   * 比如在 Objective-C 或 Swift 中，如果一个父类定义了一个方法，子类可以重写这个方法，并根据实际类型调用相应的实现。

例如，在 Objective-C 中：

```objective-c
@interface Animal : NSObject
- (void)speak;
@end

@implementation Animal
- (void)speak {
    NSLog(@"Animal makes a sound");
}
@end

@interface Dog : Animal
@end

@implementation Dog
- (void)speak {
    NSLog(@"Dog barks");
}
@end

@interface Cat : Animal
@end

@implementation Cat
- (void)speak {
    NSLog(@"Cat meows");
}
@end

// 使用多态
Animal *animal1 = [[Dog alloc] init];
Animal *animal2 = [[Cat alloc] init];
[animal1 speak]; // 输出：Dog barks
[animal2 speak]; // 输出：Cat meows
```

在这个例子中，`animal1` 和 `animal2` 的类型都是 `Animal`，但在运行时，实际的对象类型分别是 `Dog` 和 `Cat`，因此调用了它们各自的 `speak` 方法。这就是多态的一个具体体现。
