# 不可变

在 Objective-C 中，不可变数组（NSArray）一旦创建，其内容就不能被修改。

**一、创建不可变数组**

1.  使用字面量创建：

    ```objective-c
    NSArray *array = @[@"item1", @"item2", @"item3"];
    ```
2.  使用初始化方法创建：

    ```objective-c
    NSArray *array2 = [NSArray arrayWithObjects:@"obj1", @"obj2", nil];
    ```

**二、特点**

1.  不能添加、删除或替换元素：

    * 一旦创建，不能向这个数组中添加新元素，也不能删除或替换现有的元素。
    * 例如，下面的代码会导致编译错误：

    ```objective-c
    [array addObject:@"newItem"]; // 错误，不可变数组不能添加对象
    ```
2.  可以通过索引访问元素：

    * 可以使用索引来访问数组中的元素。
    * 例如：

    ```objective-c
    NSString *element = array[1];
    ```
3.  可以进行遍历：

    * 可以使用快速枚举、`NSEnumerator`或其他遍历方法来遍历不可变数组的元素。
    * 例如：

    ```objective-c
    for (NSString *item in array) {
        NSLog(@"%@", item);
    }
    ```

**三、用途**

1. 当需要一个固定的集合，不希望其内容被意外修改时，可以使用不可变数组。
2. 在多线程环境中，不可变对象通常更安全，因为不需要担心其他线程对其进行意外的修改。

**四、与可变数组的关系**

1.  可以从不可变数组创建可变数组副本：

    ```objective-c
    NSMutableArray *mutableCopy = [array mutableCopy];
    ```
2. 有时，可以先创建一个不可变数组进行初步的设置，然后根据需要创建可变副本进行修改。
