# 重写vs重载

**方法重写（Method Overriding）** 和 **函数重载（Function Overloading）** 是面向对象编程中两个不同的概念，尽管它们都涉及到方法或函数的多态性和灵活性，但它们的目的和实现方式完全不同。

#### 方法重写（Method Overriding）

**重写**是指在子类中重新定义从父类继承的方法，以提供新的实现。重写通常发生在类的继承体系中，通过重写，子类可以改变或扩展父类方法的行为。

**特点：**

1. **发生在继承关系中**：子类重写父类的方法。
2. **方法签名必须相同**：重写的方法与被重写的方法名称、参数列表和返回类型必须完全一致。
3. **多态性**：通过方法重写可以实现运行时的多态。即调用父类引用时，实际运行的是子类重写的方法。
4. **可访问父类方法**：可以通过 `super` 关键字（Java、Objective-C）或者 `base`（C#）等方式在重写的方法中调用父类的原始方法。

**例子（Java）：**

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

public class Test {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.sound();  // 输出 "Dog barks"
    }
}
```

在这个例子中，`Dog` 类重写了 `Animal` 类中的 `sound()` 方法，运行时会调用子类的方法。

#### 函数重载（Function Overloading）

**重载**是指在同一个类中定义多个具有相同名称但参数列表不同的方法或函数。编译器会根据传递的参数类型和数量来选择具体的函数或方法。

**特点：**

1. **发生在同一个类中**：多个函数或方法同名但参数列表不同。
2. **方法签名不同**：虽然函数或方法名称相同，但参数类型、参数数量或参数顺序必须不同。
3. **不依赖继承**：函数重载不需要类的继承关系，它可以发生在同一个类中。
4. **编译时多态性**：函数重载是编译时的多态，编译器在编译时决定调用哪个重载版本。

**例子（Java）：**

```java
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Test {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));         // 输出 8
        System.out.println(calc.add(5.5, 3.2));     // 输出 8.7
        System.out.println(calc.add(1, 2, 3));      // 输出 6
    }
}
```

在这个例子中，`add()` 方法被重载了三次，分别接受不同的参数类型和数量。

#### 方法重写 vs 函数重载

| **特性**   | **方法重写**          | **函数重载**          |
| -------- | ----------------- | ----------------- |
| **发生场景** | 继承关系中，子类重写父类方法    | 同一类中，多个同名方法或函数    |
| **方法签名** | 必须与父类方法相同         | 必须不同，参数类型、数量、顺序不同 |
| **多态性**  | 运行时多态，调用时根据对象类型决定 | 编译时多态，编译时根据参数决定   |
| **访问权限** | 子类不能降低父类方法的访问权限   | 不影响访问权限           |
| **返回类型** | 必须相同或父类方法返回类型的子类型 | 不需要相同             |
| **继承关系** | 需要类之间有继承关系        | 不需要继承关系           |

#### 总结

* **方法重写**发生在继承关系中，允许子类改变父类的方法行为，提供**运行时**的多态性。
* **函数重载**则发生在同一个类中，允许方法或函数名称相同但参数列表不同，提供**编译时**的多态性。
