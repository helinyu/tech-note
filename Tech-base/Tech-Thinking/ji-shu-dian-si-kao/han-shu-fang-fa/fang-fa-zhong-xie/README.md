# 方法重写

函数没有重写的概念，重写概念是面向对象中的概念。



方法重写（Method Overriding）是指在子类中重新定义从父类继承的方法，以实现不同的功能。这是面向对象编程中**多态性**的一个重要特性，使得子类能够根据具体需求修改父类中的方法行为。

#### 重写的规则

1. **方法名称相同**：重写的方法名称必须与父类中被重写的方法名称一致。
2. **参数相同**：重写的方法的参数类型和数量必须与父类中被重写的方法完全相同。
3. **返回类型相同**：在大多数编程语言中，重写方法的返回类型也必须与被重写的方法相同，某些语言允许返回类型为子类类型。
4. **访问权限不能收紧**：子类重写的方法访问权限不能比父类方法更严格。例如，父类方法是 `public`，那么子类重写时也必须是 `public`。
5. **必须存在继承关系**：重写通常发生在有继承关系的类之间，子类通过继承父类的功能，再进行自定义。

#### 使用 `super`

在重写父类方法时，通常可以通过 `super` 关键字调用父类的原始方法，从而在新的方法中保留部分父类行为。

#### 示例：Java

```java
class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

在这个例子中，`Dog` 类重写了 `Animal` 类中的 `sound` 方法，提供了不同的实现。

#### 示例：C++

```cpp
class Animal {
public:
    virtual void sound() {
        cout << "Animal makes a sound" << endl;
    }
};

class Dog : public Animal {
public:
    void sound() override {
        cout << "Dog barks" << endl;
    }
};
```

在 C++ 中，使用 `virtual` 关键字来允许方法被重写，`override` 关键字可以显式地标记重写行为。

#### 示例：Objective-C

```objc
@interface Animal : NSObject
- (void)sound;
@end

@implementation Animal
- (void)sound {
    NSLog(@"Animal makes a sound");
}
@end

@interface Dog : Animal
@end

@implementation Dog
- (void)sound {
    [super sound];  // Optional: Call the parent class method
    NSLog(@"Dog barks");
}
@end
```

在 Objective-C 中，重写父类方法也很常见，可以通过 `[super methodName]` 来调用父类的实现。

#### 方法重写 vs 方法重载

* **方法重写**：发生在父类与子类之间，子类通过相同的签名修改父类的行为。
* **方法重载**：发生在同一个类中，通过不同的参数列表来定义多个方法。

重写的目的是为了提供一种在父类基础上的扩展或特化。
