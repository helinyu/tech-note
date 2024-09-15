# 遍历

### 1、for(for..in) while(do..while) 都继承了C语言的特性 <a href="#id-1forfor..in-whiledo..while-dou-ji-cheng-lecyu-yan-de-te-xing" id="id-1forfor..in-whiledo..while-dou-ji-cheng-lecyu-yan-de-te-xing"></a>

### 2、**`NSEnumerator` 遍历 【迭代器】** <a href="#id-2nsenumerator-bian-li-die-dai-qi" id="id-2nsenumerator-bian-li-die-dai-qi"></a>

Copy

```
NSArray *array = @[@"苹果", @"香蕉", @"橘子"];
NSEnumerator *enumerator = [array objectEnumerator];
NSString *fruit;
while (fruit = [enumerator nextObject]) {
    NSLog(@"%@", fruit);
}
```

只不过，因为OC中没有元祖这个概念，所以没有同时获取索引和值。

### 3、块（Block）遍历 - `enumerateObjectsUsingBlock` <a href="#id-3-kuai-block-bian-li-enumerateobjectsusingblock" id="id-3-kuai-block-bian-li-enumerateobjectsusingblock"></a>

> 其实就是swift等现代语言中的for..in的枚举， 同时也类似foreach， 只不过它里面有stop这玩意可以停止

Copy

```
NSArray *array = @[@"苹果", @"香蕉", @"橘子"];
[array enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop) {
    NSLog(@"第 %lu 个元素是 %@", (unsigned long)idx, obj);
}];
```

[\
](https://hly-tech.gitbook.io/language/v/objective-c)
