# 不可变

在 Objective-C 中，`NSSet`是一种集合类，用于存储一组不重复的对象。

**一、创建`NSSet`**

1.  使用字面量创建：

    ```objective-c
    NSSet *set = [NSSet setWithObjects:@"obj1", @"obj2", @"obj3", nil];
    ```
2.  使用初始化方法创建：

    ```objective-c
    NSArray *array = @[@"obj1", @"obj2", @"obj3"];
    NSSet *set2 = [NSSet setWithArray:array];
    ```

**二、特点**

1.  元素唯一性：`NSSet`中的元素必须是唯一的，即不能有重复的对象。如果尝试添加重复的对象，`NSSet`会自动忽略。

    ```objective-c
    NSSet *set = [NSSet setWithObjects:@"obj1", @"obj1", @"obj2", nil];
    // set 中实际上只有 "obj1" 和 "obj2" 两个元素
    ```
2. 无序性：`NSSet`中的元素是无序的，不能通过索引来访问特定的元素。

**三、常用方法**

1.  检查是否包含特定元素：

    ```objective-c
    BOOL containsObject = [set containsObject:@"obj2"];
    ```
2.  集合的交集、并集、差集等操作：

    ```objective-c
    NSSet *set1 = [NSSet setWithObjects:@"obj1", @"obj2", @"obj3", nil];
    NSSet *set2 = [NSSet setWithObjects:@"obj2", @"obj3", @"obj4", nil];

    // 交集
    NSSet *intersectionSet = [set1 intersectSet:set2];

    // 并集
    NSSet *unionSet = [set1 unionSet:set2];

    // 差集
    NSSet *differenceSet = [set1 minusSet:set2];
    ```

**四、用途**

1.  去除重复元素：如果有一个数组包含重复的元素，可以将其转换为`NSSet`来去除重复元素，然后再转换回数组。

    ```objective-c
    NSArray *arrayWithDuplicates = @[@"obj1", @"obj2", @"obj1", @"obj3"];
    NSSet *setWithoutDuplicates = [NSSet setWithArray:arrayWithDuplicates];
    NSArray *arrayWithoutDuplicates = [setWithoutDuplicates allObjects];
    ```
2. 快速检查元素是否存在：由于`NSSet`的查找操作非常高效，可以用于快速判断一个元素是否存在于集合中。
