# 讲一下 OC 的消息机制



{% hint style="info" %}
消息发送： 类对象 —— 父类对象

消息转发：动态方法解析 —— 快速转发 —— **完整的消息转发**
{% endhint %}

Objective-C 的 **消息机制** 是其核心特性之一，也是该语言动态特性的基础。消息机制允许在运行时动态地向对象发送消息，而不是像其他语言那样在编译时确定函数调用。这种动态性使 Objective-C 强大且灵活。

#### 1. 消息发送的基本概念

在 Objective-C 中，调用方法的本质是 **向对象发送消息**。例如：

```objc
[object doSomething];
```

在这行代码中，`object` 是接收者，`doSomething` 是消息（即方法选择器）。编译器会将其转化为消息发送：

```objc
objc_msgSend(object, @selector(doSomething));
```

这表示 `object` 对象接收到 `doSomething` 这个消息，`objc_msgSend` 函数负责将消息发送给对象，执行相应的代码。

#### 2. 消息机制的底层原理

Objective-C 的消息传递机制依赖于运行时库中的函数 `objc_msgSend`。当向对象发送消息时，运行时库会进行以下步骤：

**（1）查找方法实现**

* 每个类都有一个 **类对象**，类对象中包含一个 **方法列表**，记录了该类所有可供调用的方法。
* 当发送消息时，首先会通过消息的 **选择器（selector）** 在方法列表中查找与该选择器对应的方法。
  * 选择器是方法名称的唯一标识符，它对应于一个 `SEL` 类型。
  * 运行时系统会先从接收者的类中查找对应的 `SEL`。

**（2）消息转发（Method Forwarding）**

* 如果在类中找不到对应的 `SEL`，运行时会继续沿着类继承链向上查找，直到找到该方法，或者到达 `NSObject` 类仍找不到方法为止。
* 如果最终找不到方法，程序不会直接崩溃，而是会进入 **消息转发机制**。此时，Objective-C 提供了几个拯救机会来处理未能处理的消息：
  * **动态方法解析**：通过重写 `+ (BOOL)resolveInstanceMethod:(SEL)sel` 或 `+ (BOOL)resolveClassMethod:(SEL)sel`，可以动态添加方法的实现。
  * **快速转发**：通过实现 `- (id)forwardingTargetForSelector:(SEL)aSelector`，可以将消息转发给另一个对象。
  * **完整的消息转发**：如果没有处理上述步骤，可以通过 `- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector` 返回方法签名，接着调用 `- (void)forwardInvocation:(NSInvocation *)anInvocation` 来完全自定义消息处理。

**（3）方法缓存**

* 为了提高效率，Objective-C 的运行时机制会缓存最近发送的消息的实现。当一个消息被发送时，运行时首先会在缓存中查找方法实现。如果找到缓存的实现，直接调用该实现，省去了遍历方法列表的步骤。
* 这种缓存大大提升了频繁调用消息时的性能。

#### 3. 动态绑定

* Objective-C 的消息机制是 **动态绑定** 的，即方法的调用在 **运行时** 而不是编译时确定。它不会在编译时检查方法是否存在，而是在运行时决定对象是否能够响应某个消息。这允许程序有极高的灵活性，尤其是在处理方法的动态解析和消息转发时。

#### 4. `objc_msgSend` 的工作流程

1. **发送消息**：当调用 `[object doSomething]` 时，编译器会生成一个调用 `objc_msgSend` 的指令，传递接收者对象和方法选择器。
2. **查找方法实现**：`objc_msgSend` 根据对象的类，从类的方法列表中查找对应的 `SEL`。
3. **调用实现**：如果找到实现，直接调用对应的函数指针。
4. **消息转发**：如果没有找到，进入消息转发流程。

#### 5. 消息转发机制详解

**消息转发（Message Forwarding）** 是 Objective-C 的一大特色。当一个对象接收到它不能响应的消息时，运行时会为你提供几种处理未识别消息的机制：

**（1）动态方法解析**

可以在运行时为类动态添加方法实现。例如：

```objc
+ (BOOL)resolveInstanceMethod:(SEL)sel {
    if (sel == @selector(doSomething)) {
        class_addMethod([self class], sel, (IMP)someFunction, "v@:");
        return YES;
    }
    return [super resolveInstanceMethod:sel];
}
```

通过 `class_addMethod` 可以动态地将一个函数指针绑定为类的方法实现。

**（2）快速转发**

当一个对象没有能力响应某个消息时，它可以将该消息转发给另一个对象：

```objc
- (id)forwardingTargetForSelector:(SEL)aSelector {
    if (aSelector == @selector(doSomething)) {
        return alternateObject;  // 将消息转发给 alternateObject
    }
    return [super forwardingTargetForSelector:aSelector];
}
```

**（3）完整的消息转发**

如果没有快速转发目标，可以进行完全的消息转发。首先，必须为消息生成一个方法签名，然后通过 `NSInvocation` 完成实际的转发：

```objc
- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector {
    if (aSelector == @selector(doSomething)) {
        return [NSMethodSignature signatureWithObjCTypes:"v@:"];
    }
    return [super methodSignatureForSelector:aSelector];
}

- (void)forwardInvocation:(NSInvocation *)anInvocation {
    SEL sel = [anInvocation selector];
    if ([alternateObject respondsToSelector:sel]) {
        [anInvocation invokeWithTarget:alternateObject];  // 转发消息给 alternateObject
    } else {
        [self doesNotRecognizeSelector:sel];  // 如果无法处理，抛出异常
    }
}
```

#### 6. 动态特性的优缺点

* **优点**：
  * 灵活性：允许程序动态处理消息、动态添加方法、转发消息。
  * 可扩展性：可以在运行时改变对象的行为，适用于一些动态代理和框架设计（如 CoreData、KVO）。
* **缺点**：
  * 性能：消息发送比普通函数调用稍慢，因为它涉及到运行时查找和方法分发。
  * 安全性：因为方法调用在运行时才确定，如果没有适当处理消息转发，可能导致崩溃。

#### 总结

Objective-C 的消息机制提供了高度的动态性和灵活性，允许在运行时动态决定方法调用和消息处理。它通过 `objc_msgSend` 来实现消息传递，并提供了缓存优化和消息转发机制，使得开发者能够在运行时改变对象的行为，处理未识别的消息。这是 Objective-C 的一个强大特性，广泛应用于动态代理、KVO、KVC 等机制。





