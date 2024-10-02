# 应用场景

在 Objective-C 中，`NSSet`有以下一些常见的使用场景：

### **1. 去除重复元素**

当有一个数组包含重复元素，而你想得到一个只包含唯一元素的集合时，可以使用`NSSet`。

```objective-c
NSArray *arrayWithDuplicates = @[@1, @2, @2, @3, @3, @3];
NSSet *uniqueSet = [NSSet setWithArray:arrayWithDuplicates];
NSArray *uniqueArray = [uniqueSet allObjects];
```

### **2. 快速查找元素**

`NSSet`提供了快速的查找方法`containsObject:`，可以高效地判断一个对象是否在集合中。

```objective-c
NSSet *set = [NSSet setWithObjects:@"apple", @"banana", @"orange", nil];
BOOL containsApple = [set containsObject:@"apple"];
```

### **3. 集合运算**

可以进行集合的并集、交集、差集等运算。

```objective-c
NSSet *set1 = [NSSet setWithObjects:@"A", @"B", @"C", nil];
NSSet *set2 = [NSSet setWithObjects:@"B", @"C", @"D", nil];

// 并集
NSSet *unionSet = [set1 setByAddingObjectsFromSet:set2];

// 交集
NSSet *intersectionSet = [set1 setByIntersectingSet:set2];

// 差集
NSSet *differenceSet = [set1 setBySubtractingSet:set2];
```

### **4. 存储不关心顺序的数据**

如果只关心数据的唯一性而不关心其顺序，使用`NSSet`比使用数组更合适。

例如，存储一组用户的唯一 ID：

```objective-c
NSSet *userIdsSet = [NSSet setWithObjects:@123, @456, @789, nil];
```
