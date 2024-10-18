# 重载

方法或函数重载（Method or Function Overloading）是指在同一个类中可以定义多个具有相同名称但参数不同的方法或函数。编译器根据传递的参数类型、数量、顺序来决定调用哪个重载的版本。这在面向对象编程中是一个常见的特性，用于提高代码的可读性和灵活性。

#### 重载的规则 —— <mark style="color:red;">参数</mark>判断

1. **参数类型不同**：不同重载的方法参数类型必须不同。
2. **参数个数不同**：可以通过改变参数的个数来实现重载。
3. **参数顺序不同**：如果参数类型相同，但顺序不同，也可以实现重载。

#### 重载的局限

* **返回类型不能作为重载的唯一条件**：即使方法的返回类型不同，但参数相同，编译器仍然会认为这是重复定义的函数，不能通过编译。

#### 示例：C++

```cpp
class Example {
public:
    void display(int i) {
        cout << "Integer: " << i << endl;
    }

    void display(double d) {
        cout << "Double: " << d << endl;
    }

    void display(int i, double d) {
        cout << "Integer: " << i << ", Double: " << d << endl;
    }
};
```

在上面的代码中，`display` 方法被重载了三次，分别接受不同的参数。

#### 示例：Java

```java
class Example {
    public void display(int i) {
        System.out.println("Integer: " + i);
    }

    public void display(String s) {
        System.out.println("String: " + s);
    }
}
```

#### Objective-C 中的方法重载

<mark style="color:red;">Objective-C 不支持直接的函数重载</mark>，因为方法签名中包括参数的名称。因此，如果需要实现类似重载的功能，通常通过方法命名来区分。

```objc
- (void)displayWithInt:(int)i {
    NSLog(@"Integer: %d", i);
}

- (void)displayWithString:(NSString *)str {
    NSLog(@"String: %@", str);
}
```

每个方法都有唯一的签名，因此 Objective-C 不会出现重载冲突。

