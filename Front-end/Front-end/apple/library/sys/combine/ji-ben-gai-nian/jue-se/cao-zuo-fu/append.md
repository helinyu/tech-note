# append

在 Swift 的 Combine 框架中，`append` 是一个运算符，用于将额外的元素或 Publisher 添加到当前的 Publisher 流中。当当前 Publisher 完成时，`append` 会将追加的元素或 Publisher 的内容接在原 Publisher 的后面。

#### `append` 的使用方式

1.  **追加元素**\
    `append(_:)` 可以在原 Publisher 结束后追加一个或多个元素。

    ```swift
    let numbers = [1, 2, 3].publisher
    numbers
        .append(4, 5, 6)
        .sink { print($0) }
    ```

    **输出**：

    ```
    1
    2
    3
    4
    5
    6
    ```

    在这里，`append(4, 5, 6)` 会将 `4`, `5`, 和 `6` 添加到序列的末尾。
2.  **追加 Publisher**\
    `append(Publisher)` 可以将另一个 Publisher 追加到当前 Publisher 上，当第一个 Publisher 完成后，会继续输出追加的 Publisher 的内容。

    ```swift
    let firstPublisher = [1, 2, 3].publisher
    let secondPublisher = [4, 5, 6].publisher

    firstPublisher
        .append(secondPublisher)
        .sink { print($0) }
    ```

    **输出**：

    ```
    1
    2
    3
    4
    5
    6
    ```

    在这里，当 `firstPublisher` 完成后，`secondPublisher` 的值会被追加到序列的末尾。

#### 注意事项

* `append` 只有在上一个 Publisher 发送 `.finished` 事件（即完成）后才会执行追加的内容。
* 如果第一个 Publisher 发送 `.failure`，则 `append` 不会执行。

`append` 运算符非常适合用于串联多个数据流或在流的尾部增加数据。



在 Swift 的 Combine 框架中，`append` 是一种 **组合运算符（Combining Operator）**。组合运算符的作用是将多个 Publisher 的输出合并、组合或连接，以创建一个新的数据流。`append` 正是通过在原始 Publisher 完成后，追加额外的数据或 Publisher，使流的数据更完整。

#### `append` 运算符的分类依据

* **组合运算符（Combining Operator）**：专门用于将两个或更多的 Publisher 结合到一个流中，如 `append`、`merge`、`combineLatest` 和 `zip` 等。
* 在 `append` 的操作过程中，它并不会影响原始 Publisher 的事件顺序，而是在原始 Publisher 完成后，顺序性地追加新的元素或 Publisher。

因此，`append` 是 Combine 中的一个组合运算符，通过在流的末尾添加元素或其他 Publisher 来完成组合操作。

