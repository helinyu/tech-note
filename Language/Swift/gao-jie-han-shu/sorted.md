# sorted

## 1、sorted&#x20;

对数组进行排序



### 1.1 升序排序（默认）

```
let numbers = [5, 3, 8, 1, 2]
let sortedNumbers = numbers.sorted()
print(sortedNumbers) // 输出: [1, 2, 3, 5, 8]
```

### 1.2 降序排序

```
let numbers = [5, 3, 8, 1, 2]
let sortedDescending = numbers.sorted(by: >)
print(sortedDescending) // 输出: [8, 5, 3, 2, 1]
```

### 1.3 自定义排序

```
let strings = ["apple", "pear", "banana", "grape"]
let sortedStrings = strings.sorted { $0.count < $1.count }
print(sortedStrings) // 输出: ["apple", "grape", "pear", "banana"]
```

### 1.4 对复杂类型排序

* **对自定义对象排序**：如果数组中的元素是自定义类型，可以通过指定属性进行排序。

```
struct Person {
    let name: String
    let age: Int
}

let people = [
    Person(name: "Alice", age: 30),
    Person(name: "Bob", age: 25),
    Person(name: "Charlie", age: 35)
]

let sortedPeople = people.sorted { $0.age < $1.age }
for person in sortedPeople {
    print("\(person.name): \(person.age)")
}
// 输出:
// Bob: 25
// Alice: 30
// Charlie: 35

```

## 2、sort

**原地排序**：如果你希望在原数组上进行排序，而不是返回一个新的数组，可以使用 `sort()` 方法。

```
var mutableNumbers = [5, 3, 8, 1, 2]
mutableNumbers.sort()
print(mutableNumbers) // 输出: [1, 2, 3, 5, 8]
```



{% hint style="info" %}
区别：

* `sorted()` 方法**不会修改原数组**，而是返回一个新的已排序数组。
* `sort()` 方法会**修改原数组**。
{% endhint %}



## 小结：

{% hint style="info" %}
1、sort/sorted 可以很简单的对数组进行排序

2、sort覆盖自身数组，sorted 返回数组，不改变自身

3、通过使用闭包，可以实现自定义的排序逻辑
{% endhint %}

