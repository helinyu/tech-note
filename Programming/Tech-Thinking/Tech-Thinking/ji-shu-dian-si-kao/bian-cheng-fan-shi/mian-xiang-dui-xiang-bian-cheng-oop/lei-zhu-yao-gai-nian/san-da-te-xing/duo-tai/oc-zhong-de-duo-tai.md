# OC中的多态

在 Objective-C 中，多态（Polymorphism）是面向对象编程的一个核心概念，它允许一个父类的对象在运行时表现出不同的行为。多态主要通过**继承**和\*\*方法重写（Method Overriding）\*\*来实现，允许子类提供自己的实现，从而实现动态方法调度。

在 Objective-C 中，运行时多态通过**消息传递机制**实现，这与 C++ 的虚函数表不同。Objective-C 使用的是动态类型系统，方法的具体实现直到运行时才会确定。

#### 多态的实现方式

**1. 方法重写（Method Overriding）**

在 Objective-C 中，子类可以重写父类的方法，从而在不同的对象上调用相同的方法时，表现出不同的行为。

**示例：**

```objective-c
#import <Foundation/Foundation.h>

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

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Animal *myAnimal;

        myAnimal = [[Dog alloc] init];
        [myAnimal speak];  // 输出：Dog barks

        myAnimal = [[Cat alloc] init];
        [myAnimal speak];  // 输出：Cat meows
    }
    return 0;
}
```

在这个例子中：

* `Animal` 类是父类，定义了一个 `speak` 方法。
* `Dog` 和 `Cat` 是 `Animal` 的子类，它们分别重写了 `speak` 方法。

通过父类 `Animal` 的指针 `myAnimal`，我们能够在运行时调用具体的子类方法。这是运行时多态的一个典型例子。

**2. 动态方法解析**

Objective-C 的动态特性使得它可以在运行时决定调用哪个方法。当发送消息时，Objective-C 的运行时系统会查找接收对象的方法实现，如果找到了，调用相应的实现；如果没找到，可能会触发其他动态行为（如 `forwardInvocation:`）。

**示例：**

```objective-c
#import <Foundation/Foundation.h>

@interface Bird : NSObject
@end

@implementation Bird
- (void)forwardInvocation:(NSInvocation *)anInvocation {
    NSLog(@"Unknown method %@", NSStringFromSelector([anInvocation selector]));
}
@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Bird *myBird = [[Bird alloc] init];
        [myBird performSelector:@selector(fly)];
        // 输出：Unknown method fly
    }
    return 0;
}
```

在这个例子中，当 `fly` 方法没有找到时，运行时系统调用了 `forwardInvocation:` 方法。这展示了 Objective-C 中动态方法解析的机制。

#### 3. id 类型和动态方法分派

Objective-C 中的 `id` 类型是一种动态类型，可以持有任何对象。这种动态性支持多态，因为编译器不关心 `id` 类型变量具体是什么类的对象，直到运行时才去查找具体实现。

```objective-c
#import <Foundation/Foundation.h>

@interface Car : NSObject
- (void)drive;
@end

@implementation Car
- (void)drive {
    NSLog(@"Car is driving");
}
@end

@interface Bicycle : NSObject
- (void)drive;
@end

@implementation Bicycle
- (void)drive {
    NSLog(@"Bicycle is riding");
}
@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        id vehicle;

        vehicle = [[Car alloc] init];
        [vehicle drive];  // 输出：Car is driving

        vehicle = [[Bicycle alloc] init];
        [vehicle drive];  // 输出：Bicycle is riding
    }
    return 0;
}
```

在这个例子中，`vehicle` 的类型是 `id`，它可以在运行时持有任何对象，并且通过动态分派系统在运行时决定调用哪个具体的 `drive` 方法。

#### 小结

在 Objective-C 中，多态主要通过以下机制实现：

1. **继承与方法重写**：子类可以重写父类的方法，调用时根据对象的实际类型来执行相应的方法实现。
2. **消息传递机制**：Objective-C 使用动态消息传递系统，方法的选择是在运行时完成的，而不是编译时。
3. **id 类型与动态方法分派**：通过 `id` 类型可以持有任何对象，并且在运行时动态调用方法。

这些机制使得 Objective-C 在实现多态时非常灵活，并且具有高度的动态性。
