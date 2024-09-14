# 集合

在 Haxe 中，`Set`是一种集合数据结构，用于存储一组唯一的值。

**一、创建和初始化 Set**

1. 使用构造函数创建一个空的 `Set`：

```haxe
var mySet = new haxe.ds.Set<Int>();
```

这里创建了一个存储整数类型元素的 `Set`。

2. 使用数组字面量初始化一个 `Set`：

```haxe
var initialSet = new haxe.ds.Set([1, 2, 3]);
```

**二、基本操作**

1. 添加元素：

```haxe
mySet.add(4);
```

2. 检查元素是否存在：

```haxe
if (mySet.exists(4)) {
    trace("Element 4 exists in the set.");
}
```

3. 删除元素：

```haxe
mySet.remove(4);
```

4. 获取集合大小：

```haxe
var size = mySet.length;
trace("Set size: " + size);
```

**三、遍历 Set**

可以使用 `for..in` 循环遍历 `Set` 的元素：

```haxe
for (element in mySet) {
    trace(element);
}
```

**四、Set 的特点**

1. 唯一性：`Set` 中的元素是唯一的，重复添加相同的元素不会增加集合的大小。
2. 高效的查找：可以快速检查一个元素是否存在于 `Set` 中。

例如，以下代码可以去除数组中的重复元素并存储在 `Set` 中：

```haxe
var arrayWithDuplicates = [1, 2, 2, 3, 3, 3];
var uniqueSet = new haxe.ds.Set(arrayWithDuplicates);
trace(uniqueSet);
```

`Set` 在 Haxe 中常用于需要存储唯一值的场景，如去除重复数据、快速查找等。
