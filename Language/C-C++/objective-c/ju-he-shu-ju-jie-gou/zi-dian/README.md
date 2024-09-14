# 字典

在 Objective-C 中，字典（NSDictionary 和 NSMutableDictionary）用于存储键值对。

**一、不可变字典（NSDictionary）**

1. 创建不可变字典：
   *   使用字面量创建：

       ```objective-c
       NSDictionary *dictionary = @{@"key1" : @"value1", @"key2" : @"value2"};
       ```
   *   使用初始化方法创建：

       ```objective-c
       NSDictionary *dictionary2 = [NSDictionary dictionaryWithObjectsAndKeys:@"value1", @"key1", @"value2", @"key2", nil];
       ```
2. 特点：
   * 一旦创建，内容不能被修改。不能添加、删除或修改键值对。
   *   例如，下面的代码会导致编译错误：

       ```objective-c
       [dictionary setObject:@"newValue" forKey:@"key1"]; // 错误，不可变字典不能修改
       ```
3. 访问键值对：
   *   通过键获取对应的值：

       ```objective-c
       NSString *value = dictionary[@"key1"];
       ```
   *   检查字典中是否包含特定的键：

       ```objective-c
       BOOL containsKey = [dictionary containsKey:@"key3"];
       ```

**二、可变字典（NSMutableDictionary）**

1. 创建可变字典：
   *   使用初始化方法创建：

       ```objective-c
       NSMutableDictionary *mutableDictionary = [[NSMutableDictionary alloc] init];
       ```
2. 添加键值对：
   *   使用 `setObject:forKey:` 方法添加键值对：

       ```objective-c
       [mutableDictionary setObject:@"value1" forKey:@"key1"];
       ```
3. 删除键值对：
   *   通过键删除键值对：

       ```objective-c
       [mutableDictionary removeObjectForKey:@"key1"];
       ```
4. 修改键值对：
   *   可以直接使用 `setObject:forKey:` 方法修改已有键对应的值：

       ```objective-c
       [mutableDictionary setObject:@"newValue" forKey:@"key1"];
       ```

**三、用途**

1. 存储和检索数据：字典可以方便地根据键来存储和检索值，适用于需要快速查找特定键对应的值的场景。
2. 配置信息：可以将配置参数存储在字典中，方便在程序中读取和使用。
3. 数据模型：可以用字典来表示复杂的数据结构，例如 JSON 数据的解析结果。

**四、注意事项**

1. 键的类型：字典的键通常是不可变对象，如 NSString、NSNumber 等。如果使用可变对象作为键，可能会导致不可预测的行为。
2. 内存管理：如果字典中的值是对象，需要根据所有权关系进行适当的内存管理，例如使用 `retain`、`copy` 或遵循正确的内存管理规则。
