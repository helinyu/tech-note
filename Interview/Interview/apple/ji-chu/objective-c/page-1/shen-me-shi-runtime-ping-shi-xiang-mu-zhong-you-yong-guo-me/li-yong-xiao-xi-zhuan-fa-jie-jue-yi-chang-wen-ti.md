# 利用消息转发解决异常问题

在 Objective-C 中，当你调用一个对象的方法时，如果该对象没有实现该方法，会抛出 `NSInvalidArgumentException` 异常。为了优雅地处理这种情况，可以利用消息转发机制。

#### 消息转发机制

1. **动态方法解析**：在运行时，你可以通过 `+resolveInstanceMethod:` 或 `+resolveClassMethod:` 方法动态地为实例或类添加实现。
2. **普通转发**：如果某个方法未被实现，可以重写 `-forwardInvocation:` 方法，将消息转发到其他对象。
3. **目标选择**：使用 `-methodSignatureForSelector:` 方法来提供方法的签名。

#### 代码示例

下面是一个使用消息转发机制的示例，展示了如何优雅地处理找不到方法的异常：

```objc
#import <Foundation/Foundation.h>

@interface MyClass : NSObject
@end

@implementation MyClass

// 当接收到未实现的方法时，使用该方法转发
- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector {
    // 如果方法没有被实现，返回一个默认的签名
    if ([NSStringFromSelector(aSelector] isEqualToString:@"dynamicMethod:"]) {
        return [NSMethodSignature signatureWithObjCTypes:"@:@"];
    }
    return [super methodSignatureForSelector:aSelector];
}

// 方法转发
- (void)forwardInvocation:(NSInvocation *)anInvocation {
    // 判断要转发的方法
    if ([NSStringFromSelector(anInvocation.selector) isEqualToString:@"dynamicMethod:"]) {
        // 执行你希望的逻辑
        NSLog(@"Forwarding to dynamicMethod:");
        
        // 你可以传入参数
        NSString *argument = nil;
        [anInvocation getArgument:&argument atIndex:2]; // 第一个参数索引为2
        NSLog(@"Argument: %@", argument);
        
        // 返回一个结果
        NSString *result = [NSString stringWithFormat:@"Received: %@", argument];
        [anInvocation setReturnValue:&result];
    } else {
        [super forwardInvocation:anInvocation];
    }
}

@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        MyClass *obj = [[MyClass alloc] init];
        // 这会触发转发机制
        [obj performSelector:@selector(dynamicMethod:) withObject:@"Hello"];
    }
    return 0;
}
```

#### 代码解释

1. **methodSignatureForSelector:**
   * 当尝试调用 `dynamicMethod:` 方法时，如果 `MyClass` 没有实现该方法，它会返回一个默认的签名，表示该方法是可用的。
2. **forwardInvocation:**
   * 当消息被发送到未实现的方法时，这个方法会被调用。在这里，你可以定义要执行的逻辑。
   * 示例中，打印参数并返回一个字符串结果。
3. **main函数:**
   * 创建 `MyClass` 的实例并调用 `dynamicMethod:` 方法。

#### 运行结果

程序会输出：

```
Forwarding to dynamicMethod:
Argument: Hello
```

这样，就通过消息转发机制处理了找不到方法的情况，从而避免了异常的抛出。
