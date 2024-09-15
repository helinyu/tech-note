# 可变

在 Objective-C（OC）中，**可变字典（NSMutableDictionary）** 是一个能够存储键值对并允许动态添加、删除、修改键值对的集合。它是 `NSDictionary` 的可变版本。与不可变字典不同，`NSMutableDictionary` 允许你在创建字典之后修改其内容。

#### 创建可变字典

**1. 空的可变字典**

```objective-c
NSMutableDictionary *dict = [NSMutableDictionary dictionary];
```

**2. 初始化带有初始值的可变字典**

```objective-c
NSMutableDictionary *dict = [NSMutableDictionary dictionaryWithObjectsAndKeys:
                              @"value1", @"key1",
                              @"value2", @"key2", nil];
```

#### 常用操作

**1. 添加键值对**

可以通过 `setObject:forKey:` 方法向字典中添加键值对。如果键已经存在，会更新对应的值。

```objective-c
[dict setObject:@"newValue" forKey:@"newKey"];
```

例如：

```objective-c
NSMutableDictionary *dict = [NSMutableDictionary dictionary];
[dict setObject:@"Objective-C" forKey:@"language"];
NSLog(@"%@", dict);  // 输出：{ language = "Objective-C"; }
```

**2. 删除键值对**

使用 `removeObjectForKey:` 可以删除字典中的某个键值对：

```objective-c
[dict removeObjectForKey:@"key1"];
```

也可以删除所有的键值对：

```objective-c
[dict removeAllObjects];
```

**3. 修改值**

如果字典中已经存在某个键，可以直接通过 `setObject:forKey:` 来更新对应的值。例如：

```objective-c
[dict setObject:@"Swift" forKey:@"language"];  // 修改键为 "language" 的值
```

**4. 获取值**

你可以使用 `objectForKey:` 来获取某个键对应的值：

```objective-c
NSString *value = [dict objectForKey:@"key1"];
```

从 iOS 6 开始，你也可以使用下标语法来获取或设置值：

```objective-c
NSString *value = dict[@"key1"];   // 获取值
dict[@"key2"] = @"newValue";       // 设置值
```

**5. 获取所有键或值**

你可以获取所有的键或值：

```objective-c
NSArray *allKeys = [dict allKeys];     // 获取所有的键
NSArray *allValues = [dict allValues]; // 获取所有的值
```

#### 示例

以下是一个综合示例，演示如何创建、修改和操作可变字典：

```objective-c
NSMutableDictionary *dict = [NSMutableDictionary dictionaryWithObjectsAndKeys:
                             @"Apple", @"company",
                             @"iPhone", @"product", nil];

// 添加新的键值对
[dict setObject:@"Objective-C" forKey:@"language"];

// 修改现有的键值对
[dict setObject:@"MacBook" forKey:@"product"];

// 获取值
NSString *company = [dict objectForKey:@"company"];
NSLog(@"Company: %@", company);  // 输出：Company: Apple

// 删除键值对
[dict removeObjectForKey:@"language"];

// 使用下标语法
dict[@"OS"] = @"macOS";
NSLog(@"%@", dict);  // 输出：{ company = Apple; OS = macOS; product = MacBook; }
```

#### 注意事项

1. **键的唯一性**：在字典中，键必须是唯一的。如果使用相同的键多次添加，会覆盖原有的值。
2. **键的类型**：字典的键必须是对象类型（如 `NSString`、`NSNumber` 等），不能是基本类型（如 `int`、`float` 等）。
