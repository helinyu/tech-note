# 可变

在 Objective-C 中，可变数组（NSMutableArray）可以动态地添加、删除和修改元素。

**一、创建可变数组**

1.  使用初始化方法创建：

    ```objective-c
    NSMutableArray *array = [[NSMutableArray alloc] init];
    ```
2.  使用字面量创建并强制转换为可变数组：

    ```objective-c
    NSMutableArray *array2 = [@[@"item1", @"item2", @"item3"] mutableCopy];
    ```

**二、添加元素**

1.  在末尾添加单个元素：

    ```objective-c
    [array addObject:@"newItem"];
    ```
2.  在指定位置插入单个元素：

    ```objective-c
    [array insertObject:@"insertedItem" atIndex:1];
    ```
3.  添加多个元素：

    ```objective-c
    NSArray *moreItems = @[@"item4", @"item5"];
    [array addObjectsFromArray:moreItems];
    ```

**三、删除元素**

1.  删除指定位置的元素：

    ```objective-c
    [array removeObjectAtIndex:0];
    ```
2.  删除特定元素：

    ```objective-c
    [array removeObject:@"item2"];
    ```
3.  删除所有元素：

    ```objective-c
    [array removeAllObjects];
    ```

**四、修改元素**

1.  通过索引修改元素：

    ```objective-c
    [array replaceObjectAtIndex:1 withObject:@"replacedItem"];
    ```

**五、其他操作**

1.  快速枚举遍历：

    ```objective-c
    for (id item in array) {
        NSLog(@"%@", item);
    }
    ```
2.  获取元素数量：

    ```objective-c
    NSUInteger count = [array count];
    ```
3.  检查是否包含特定元素：

    ```objective-c
    BOOL containsItem = [array containsObject:@"specificItem"];
    ```

**六、用途**

可变数组在需要动态管理集合内容的情况下非常有用。例如，存储用户输入的数据、管理动态生成的对象列表等。
