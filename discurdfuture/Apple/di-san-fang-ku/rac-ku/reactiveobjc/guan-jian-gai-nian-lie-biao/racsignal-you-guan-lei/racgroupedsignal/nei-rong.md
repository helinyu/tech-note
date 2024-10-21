# 内容

`RACGroupedSignal` 是 ReactiveCocoa 中的一个辅助类型，通常作为 `groupBy:` 操作符的结果出现，用于将一个信号的事件按照某种特定的规则进行分组。分组后的信号通过 `RACGroupedSignal` 传递，每个 `RACGroupedSignal` 实例表示一个特定的分组，订阅者可以根据分组进行进一步的事件处理。

#### `RACGroupedSignal` 的特点

1. **分组标识**：`RACGroupedSignal` 包含一个 `key` 属性，表示当前分组的标识，通常是根据某个条件（如对象属性、值等）生成的。
2. **基于 `groupBy:` 操作生成**：`RACGroupedSignal` 由信号的 `groupBy:` 操作生成，通常是对原始信号的元素进行分类后生成的分组信号。
3. **同一分组**：在同一个 `RACGroupedSignal` 实例中，所有的事件都是属于同一个分组的。
4. **独立处理**：每个 `RACGroupedSignal` 可以独立地进行处理和订阅，支持对不同分组进行差异化处理。

#### `groupBy:` 操作生成 `RACGroupedSignal`

`groupBy:` 操作符用于将一个信号的元素按特定的键分组，并返回一个信号，该信号会发送 `RACGroupedSignal` 类型的事件。每个 `RACGroupedSignal` 实例代表一个特定的分组，且包含一个唯一的 `key`。

#### 使用示例

以下示例展示了如何使用 `groupBy:` 将一个信号的事件按条件进行分组，并对不同分组的信号进行处理。

**1. 基本使用**

假设有一个信号 `numbersSignal`，发送一组整数。我们可以通过 `groupBy:` 将这些整数按奇偶分组，并对不同的分组进行处理：

```objc
// 创建一个信号，发送一组整数
RACSignal *numbersSignal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {
    [subscriber sendNext:@1];
    [subscriber sendNext:@2];
    [subscriber sendNext:@3];
    [subscriber sendNext:@4];
    [subscriber sendCompleted];
    return nil;
}];

// 使用 groupBy: 将信号按奇偶分组
RACSignal *groupedSignal = [numbersSignal groupBy:^id(NSNumber *number) {
    return (number.intValue % 2 == 0) ? @"Even" : @"Odd";
}];

// 订阅分组信号
[groupedSignal subscribeNext:^(RACGroupedSignal *groupedSignal) {
    NSLog(@"Group: %@", groupedSignal.key);
    
    // 针对每个分组的信号进行订阅
    [groupedSignal subscribeNext:^(id x) {
        NSLog(@"%@ Group - Value: %@", groupedSignal.key, x);
    }];
}];
```

输出：

```
Group: Odd
Odd Group - Value: 1
Odd Group - Value: 3
Group: Even
Even Group - Value: 2
Even Group - Value: 4
```

在这个例子中，`numbersSignal` 按奇偶性分成了 `Odd` 和 `Even` 两个分组，`groupBy:` 为每个分组生成了一个 `RACGroupedSignal`，我们可以根据 `key`（`Odd` 和 `Even`）识别不同的分组并分别处理每个组内的事件。

**2. 针对不同分组做不同的处理**

使用 `RACGroupedSignal` 的 `key` 属性，可以根据分组做出不同的反应：

```objc
[groupedSignal subscribeNext:^(RACGroupedSignal *groupedSignal) {
    if ([groupedSignal.key isEqualToString:@"Odd"]) {
        [groupedSignal subscribeNext:^(id x) {
            NSLog(@"Odd Number: %@", x);
        }];
    } else if ([groupedSignal.key isEqualToString:@"Even"]) {
        [groupedSignal subscribeNext:^(id x) {
            NSLog(@"Even Number: %@", x);
        }];
    }
}];
```

输出：

```
Odd Number: 1
Odd Number: 3
Even Number: 2
Even Number: 4
```

在这里，通过 `key` 判断分组类型，并对 `Odd` 和 `Even` 组进行不同的处理。

#### 总结

* `RACGroupedSignal` 用于 `groupBy:` 操作后的信号分组，包含一个 `key` 标识分组。
* 每个 `RACGroupedSignal` 实例代表一个特定的分组，所有分组事件都通过这个分组信号传递。
* 可以基于 `key` 属性对不同的分组做出不同处理，从而实现对信号流的精细化管理。

`RACGroupedSignal` 非常适合在需要根据特定条件对信号进行分组和分类处理的场景中使用，例如按用户类型、数据属性等条件对事件流进行逻辑分流。
