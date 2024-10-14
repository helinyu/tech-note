# OC

在 Objective-C 中，协变（Covariance）和逆变（Contravariance）通常与<mark style="color:red;">泛型和类型转换相关</mark>。

#### 协变（Covariance）

协变允许你在返回类型上使用子类。下面是一个简单的示例，展示了协变的概念：

```objc
// 定义一个基类
@interface Animal : NSObject
- (NSString *)makeSound;
@end

@implementation Animal
- (NSString *)makeSound {
    return @"Some generic animal sound";
}
@end

// 定义一个子类
@interface Dog : Animal
- (NSString *)makeSound;
@end

@implementation Dog
- (NSString *)makeSound {
    return @"Woof";
}
@end

// 定义一个泛型方法
@interface Shelter : NSObject
- (Animal *)adoptAnimal; // 返回类型为 Animal，协变
@end

@implementation Shelter
- (Animal *)adoptAnimal {
    return [[Dog alloc] init]; // 返回 Dog 类型的实例
}
@end

// 使用示例
Shelter *shelter = [[Shelter alloc] init];
Animal *animal = [shelter adoptAnimal];
NSLog(@"%@", [animal makeSound]); // 输出: Woof
```

在这个例子中，`Shelter` 类的方法 `adoptAnimal` 返回一个 `Animal` 类型，但实际上返回的是 `Dog` 类型的实例，展示了协变的使用。

#### 逆变（Contravariance）

逆变通常用于参数类型，可以让你在参数类型上使用父类。下面是一个简单的示例：

```objc
// 定义一个基类
@interface Shape : NSObject
@end

@implementation Shape
@end

// 定义一个子类
@interface Circle : Shape
@end

@implementation Circle
@end

// 定义一个处理形状的类
@interface ShapeHandler : NSObject
- (void)handleShape:(Shape *)shape; // 参数类型为 Shape，逆变
@end

@implementation ShapeHandler
- (void)handleShape:(Shape *)shape {
    NSLog(@"Handling shape");
}
@end

// 使用示例
ShapeHandler *handler = [[ShapeHandler alloc] init];
Circle *circle = [[Circle alloc] init];

// 传递子类实例，符合逆变原则
[handler handleShape:circle]; // 输出: Handling shape
```

在这个例子中，`ShapeHandler` 类的方法 `handleShape:` 接受一个 `Shape` 类型的参数，但你可以传递 `Circle` 类型的实例，展示了逆变的使用。

#### 总结

* **协变**：在返回类型上允许使用子类（如 `adoptAnimal` 返回 `Dog` 类型的实例作为 `Animal` 类型）。
* **逆变**：在参数类型上允许使用父类（如 `handleShape:` 接受 `Shape` 类型的参数，但可以传递 `Circle` 类型的实例）。

希望这些示例能帮助您理解协变和逆变在 Objective-C 中的具体使用！如果您有其他问题，请随时问我。
