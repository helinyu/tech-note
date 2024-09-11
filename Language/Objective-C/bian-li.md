# 遍历

## 1、for(for..in) while(do..while) 都继承了C语言的特性



## 2、**`NSEnumerator` 遍历 ， 类似swift等其他语言的for..in(**enumerated**)**&#x20;

```
NSArray *array = @[@"苹果", @"香蕉", @"橘子"];
NSEnumerator *enumerator = [array objectEnumerator];
NSString *fruit;
while (fruit = [enumerator nextObject]) {
    NSLog(@"%@", fruit);
}
```

只不过，因为OC中没有元祖这个概念，所以没有同时获取索引和值。



## 3、块（Block）遍历 - `enumerateObjectsUsingBlock`

> 其实就是swift等现代语言中的for..in的枚举， 同时也类似foreach， 只不过它里面有stop这玩意可以停止

```
NSArray *array = @[@"苹果", @"香蕉", @"橘子"];
[array enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop) {
    NSLog(@"第 %lu 个元素是 %@", (unsigned long)idx, obj);
}];
```
