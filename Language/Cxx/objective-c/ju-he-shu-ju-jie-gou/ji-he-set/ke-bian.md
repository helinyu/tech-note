# 可变

在 Objective-C 中，**可变集合（NSMutableSet）** 是一种无序的集合，能够存储唯一的对象并允许动态添加、删除和修改其内容。它是 `NSSet` 的可变版本，`NSMutableSet` 继承自 `NSSet`，允许集合在创建后修改。

#### 可变集合的特点

* **唯一性**：集合中的每个对象都是唯一的，重复的对象不会被添加。
* **无序性**：集合中的对象没有顺序，不能通过索引访问。

#### 创建可变集合

1.  **空的可变集合**：

    ```objective-c
    NSMutableSet *set = [NSMutableSet set];
    ```
2.  **使用现有集合初始化**：

    ```objective-c
    NSSet *initialSet = [NSSet setWithObjects:@"Apple", @"Google", @"Microsoft", nil];
    NSMutableSet *mutableSet = [NSMutableSet setWithSet:initialSet];
    ```

#### 常用操作

**1. 添加对象**

使用 `addObject:` 方法可以向集合中添加一个对象。如果对象已经存在，集合不会进行任何操作。

```objective-c
[mutableSet addObject:@"Facebook"];
```

例如：

```objective-c
NSMutableSet *set = [NSMutableSet set];
[set addObject:@"Apple"];
[set addObject:@"Google"];
NSLog(@"%@", set);  // 输出的顺序是无序的
```

**2. 删除对象**

*   **删除指定对象**： 使用 `removeObject:` 方法可以删除集合中的指定对象：

    ```objective-c
    [mutableSet removeObject:@"Google"];
    ```
*   **删除所有对象**： 使用 `removeAllObjects` 可以清空集合中的所有元素：

    ```objective-c
    [mutableSet removeAllObjects];
    ```

**3. 修改集合内容**

集合中的对象是唯一的，因此不需要特别的“修改”操作。如果你想更新集合中的某个对象，实际上是先删除该对象，然后添加一个新的对象。由于集合中的对象必须是唯一的，添加重复的对象不会改变集合。

**4. 获取集合中的元素**

虽然集合是无序的，不能通过索引来访问元素，但可以使用一些方法获取集合中的对象：

*   **枚举所有元素**：

    ```objective-c
    for (NSString *item in mutableSet) {
        NSLog(@"%@", item);
    }
    ```
*   **检查是否包含对象**： 使用 `containsObject:` 可以检查集合中是否包含某个对象：

    ```objective-c
    if ([mutableSet containsObject:@"Apple"]) {
        NSLog(@"Set contains Apple");
    }
    ```
*   **获取集合中的所有元素**： 可以使用 `allObjects` 将集合中的元素转换为一个数组，虽然顺序仍然不固定：

    ```objective-c
    NSArray *arrayFromSet = [mutableSet allObjects];
    ```

**5. 集合运算**

*   **并集**：使用 `unionSet:` 方法将另一个集合的元素添加到当前集合中（会自动去重）：

    ```objective-c
    NSSet *anotherSet = [NSSet setWithObjects:@"Facebook", @"Amazon", nil];
    [mutableSet unionSet:anotherSet];
    ```
*   **交集**：使用 `intersectSet:` 方法可以保留两个集合中的共同元素：

    ```objective-c
    NSSet *anotherSet = [NSSet setWithObjects:@"Apple", @"Amazon", nil];
    [mutableSet intersectSet:anotherSet];
    ```
*   **差集**：使用 `minusSet:` 方法可以从当前集合中删除另一个集合中的元素：

    ```objective-c
    NSSet *anotherSet = [NSSet setWithObjects:@"Google", @"Microsoft", nil];
    [mutableSet minusSet:anotherSet];
    ```

#### 示例

以下是一个综合的示例，展示了如何创建、操作和运算可变集合：

```objective-c
NSMutableSet *set = [NSMutableSet setWithObjects:@"Apple", @"Google", @"Microsoft", nil];

// 添加对象
[set addObject:@"Facebook"];
NSLog(@"Set: %@", set);

// 删除对象
[set removeObject:@"Microsoft"];
NSLog(@"After removal: %@", set);

// 检查是否包含对象
if ([set containsObject:@"Google"]) {
    NSLog(@"Set contains Google");
}

// 集合运算 - 并集
NSSet *newSet = [NSSet setWithObjects:@"Amazon", @"Google", nil];
[set unionSet:newSet];
NSLog(@"After union: %@", set);

// 集合运算 - 交集
NSSet *anotherSet = [NSSet setWithObjects:@"Apple", @"Amazon", nil];
[set intersectSet:anotherSet];
NSLog(@"After intersection: %@", set);

// 集合运算 - 差集
[set minusSet:[NSSet setWithObjects:@"Apple", nil]];
NSLog(@"After minus: %@", set);
```

#### 注意事项

* `NSMutableSet` 的元素必须是唯一的对象，且通常为 `NSObject` 的子类。
* 和其他集合类一样，`NSMutableSet` 不保存对象的顺序，也不能通过索引访问元素。
