# 去重

在 `Combine` 中，`removeDuplicates` 确实只能移除**连续**的相同值。如果想要移除所有重复的值（无论它们是否连续出现），需要使用自定义的解决方案。例如，可以使用 `scan` 和 `filter` 操作符，结合一个集合来追踪已经发出的唯一值，从而移除所有的重复项。

#### 示例：移除所有重复的值

以下示例展示了如何使用 `scan` 和 `filter` 来移除所有重复的值：

```swift
import Combine

let numbers = [1, 2, 2, 3, 1, 4, 3, 5, 4, 6].publisher

let uniqueValuesSubscription = numbers
    .scan(into: Set<Int>()) { seenValues, newValue in
        seenValues.insert(newValue) // 使用集合追踪已处理的值
    }
    .filter { seenValues, newValue in
        seenValues.insert(newValue).inserted // 如果新值是集合中未出现过的，则保留
    }
    .map { $0 } // 只保留唯一的值
    .sink { value in
        print(value) // 输出: 1, 2, 3, 4, 5, 6
    }
```

在这个示例中：

* `scan(into:)` 使用一个 `Set` 来跟踪已处理的值。
* 每次发出一个新值时，`filter` 会检查该值是否已存在于集合中。如果是新值，则会保留；否则，将被过滤掉。
* 最后，通过 `sink` 输出所有去重后的值。

#### 简化示例

如果想要更简单的解决方案，可以直接将每个值放入集合中，并根据是否首次出现进行过滤：

```swift
let uniqueValuesSubscription = numbers
    .filter { value in
        !seenValues.contains(value) ? seenValues.insert(value) != nil : false
    }
    .sink { value in
        print(value) // 输出: 1, 2, 3, 4, 5, 6
    }
```

这种方式可以有效移除所有重复的值，使得数据流中只包含唯一项。
