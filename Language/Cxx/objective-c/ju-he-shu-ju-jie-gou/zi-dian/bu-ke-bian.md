# 不可变

在 Objective-C 中，不可变字典（`NSDictionary`）是一种存储键值对的集合，一旦创建后其内容不能被修改。

**一、创建不可变字典**

1.  使用字面量创建：

    ```objective-c
    NSDictionary *dictionary = @{@"key1" : @"value1", @"key2" : @"value2"};
    ```
2.  使用初始化方法创建：

    ```objective-c
    NSDictionary *dictionary2 = [NSDictionary dictionaryWithObjectsAndKeys:@"value1", @"key1", @"value2", @"key2", nil];
    ```

    或者：

    ```objective-c
    NSArray *keys = @[@"key1", @"key2"];
    NSArray *values = @[@"value1", @"value2"];
    NSDictionary *dictionary3 = [NSDictionary dictionaryWithObjects:values forKeys:keys];
    ```

**二、特点**

1.  内容不可修改：一旦创建，不能添加、删除或修改键值对。尝试对不可变字典进行修改操作会导致编译错误或运行时异常。

    ```objective-c
    [dictionary setObject:@"newValue" forKey:@"key1"]; // 编译错误，不可变字典不能修改
    ```
2. 线程安全：在多线程环境下，不可变字典通常是线程安全的，因为其内容不会被意外修改。多个线程可以安全地访问不可变字典而无需额外的同步机制。
3. 高效性：由于不可变字典的内容不会改变，系统可以进行一些优化，在某些情况下可能比可变字典更高效。

**三、访问键值对**

1.  通过键获取值：

    ```objective-c
    NSString *value = dictionary[@"key1"];
    ```
2.  检查字典中是否包含特定键：

    ```objective-c
    BOOL containsKey = [dictionary containsKey:@"key3"];
    ```

**四、用途**

1. 存储固定的配置信息：例如应用程序的设置、常量数据等，这些数据在程序运行期间不需要被修改。
2. 作为函数的返回值：如果一个函数需要返回一组键值对，但不希望调用者能够修改这些数据，可以返回一个不可变字典。
3. 传递数据：在不同的对象之间传递数据时，如果数据不需要被修改，可以使用不可变字典来确保数据的完整性。
