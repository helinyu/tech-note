# 三大特性

面向对象编程（OOP）的三大特性是**封装**、**继承**和**多态**。这些特性为开发者提供了一种模块化、灵活的编程方式。

#### 1. 封装（Encapsulation）

封装是指将数据（属性）和操作数据的方法（函数或方法）封装在一起，使数据仅能通过特定的接口进行访问。封装通过控制属性的访问权限，确保对象内部状态的安全性和一致性，防止外部代码直接修改对象的状态。

* **优点**：
  * 提高了代码的安全性和可维护性。
  * 外界无法直接访问对象内部的数据，减少了代码的耦合性。
* **实现方式**：
  * 通过访问控制符，如`private`、`protected`、`public`，控制数据的访问范围。
  * 提供公共的`getter`和`setter`方法来访问和修改私有属性。

**例子**：

```objective-c
@interface Person : NSObject
@property (nonatomic, strong) NSString *name;
@property (nonatomic, assign) int age;
@end
@implementation Person
// 通过getter和setter访问封装的属性
@end
```

#### 2. 继承（Inheritance）

继承允许一个类从另一个类获得属性和方法，形成父类和子类的关系。子类继承了父类的特性，可以复用父类的代码，并可以扩展或修改父类的行为。

* **优点**：
  * 提高代码的可重用性。
  * 子类能够继承父类的功能，减少重复代码。
* **实现方式**：
  * 在子类中声明继承父类，子类自动拥有父类的属性和方法。
  * 子类可以重写（override）父类的方法，以提供不同的实现。

**例子**：

```objective-c
@interface Animal : NSObject
- (void)makeSound;
@end
@implementation Animal
- (void)makeSound {
    NSLog(@"Animal sound");
}
@end

@interface Dog : Animal
@end
@implementation Dog
- (void)makeSound {
    NSLog(@"Bark");
}
@end
```

#### 3. 多态（Polymorphism）

多态允许对象以不同的形式表现，即同一个方法在不同的对象中可以有不同的实现。通过多态，父类的引用可以指向子类对象，执行时根据实际对象类型调用对应的方法。

* **优点**：
  * 提高了代码的灵活性和扩展性。
  * 使得同一个接口可以根据具体对象的类型表现出不同的行为。
* **实现方式**：
  * 方法重写：子类可以重写父类的方法，提供不同的实现。
  * 接口实现：在不同的类中实现同一个接口。

**例子**：

```objective-c
Animal *animal = [[Dog alloc] init];
[animal makeSound]; // 输出 "Bark"
```

在这个例子中，虽然`animal`被声明为`Animal`类型，但由于它实际上指向`Dog`对象，调用的是`Dog`类的`makeSound`方法。这就是多态的表现。
