# merge、zip、combineLatest 和 switchToLatest

以下是 `merge`、`zip`、`combineLatest` 和 `switchToLatest` 在 `Combine` 中的对比：

| 特性                     | `merge`                                        | `zip`                                            | `combineLatest`                                          | `switchToLatest`                                      |
| ---------------------- | ---------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------- | ----------------------------------------------------- |
| **作用**                 | 将多个 `Publisher` 合并成一个流，按顺序发出所有 `Publisher` 的值。 | 将多个 `Publisher` 的值一一配对，按顺序发出每个 `Publisher` 的最新值。 | 将多个 `Publisher` 的最新值合并，任何一个 `Publisher` 发出新值时都会触发新的组合输出。 | 在多个 `Publisher` 中动态切换，始终只订阅最新的 `Publisher`。           |
| **发出值的条件**             | 每个 `Publisher` 中的值会被按顺序发出。                     | 所有 `Publisher` 的最新值会按顺序发出。                       | 任意一个 `Publisher` 发出新值时，都会发出当前所有 `Publisher` 的最新值。        | 外层 `Publisher` 发出一个新的内部 `Publisher` 时，切换并订阅它。         |
| **处理多个 Publisher**     | 合并多个 `Publisher`，并按顺序发出它们的值。                   | 将多个 `Publisher` 的值配对，形成元组，一一发出。                  | 始终保留所有 `Publisher` 的最新值，每次更新时都会发出新的组合结果。                 | 始终只订阅最新发出的 `Publisher`，并丢弃其他的。                        |
| **值的顺序**               | 保持各个 `Publisher` 的顺序发出值。                       | 保证值的顺序是一一对应的。                                    | 保证发出的值是每个 `Publisher` 的最新值。                              | 始终关注当前活动的 `Publisher`，只发出该 `Publisher` 的值。            |
| **等待所有 Publisher 发出值** | 否，所有 `Publisher` 发出的值都会被立刻合并发出。                | 是，`zip` 需要每个 `Publisher` 发出一个值后才会发出组合元组。         | 否，`combineLatest` 只要任何一个 `Publisher` 发出新值就会发出新的组合值。      | 否，`switchToLatest` 只发出当前最新的 `Publisher` 的值，切换时丢弃先前的值。 |
| **适用场景**               | 用于多个流的数据合并处理，不关注同步。                            | 用于需要同步多个流的场景，保证顺序和配对。                            | 用于需要实时合并多个流的最新值的场景。                                      | 用于动态选择最新流，通常适用于动态请求或事件流。                              |
| **完成行为**               | 一旦所有 `Publisher` 完成，`merge` 完成。                | 一旦任何一个 `Publisher` 完成，`zip` 完成。                  | 一旦任何一个 `Publisher` 完成，`combineLatest` 停止发出值。             | 一旦内层 `Publisher` 完成，`switchToLatest` 会停止发出值。          |

#### 主要差异总结：

1. **发出值的时机**：
   * `merge` 会立刻发出每个 `Publisher` 的值，所有流的值会并行发出。
   * `zip` 会等待所有 `Publisher` 都发出新值时才会发出配对的结果。
   * `combineLatest` 会在任何一个 `Publisher` 发出新值时触发，发出所有 `Publisher` 当前的最新值。
   * `switchToLatest` 只关注外层 `Publisher` 发出的最新内层 `Publisher` 的值，切换时丢弃其他内层 `Publisher` 的输出。
2. **适用场景**：
   * `merge` 适合并行处理多个流的场景，数据流不需要严格同步。
   * `zip` 适合需要同步且按顺序匹配多个流的场景，确保每个流都提供值。
   * `combineLatest` 适合合并多个流的最新数据，每当有更新时就发出新的组合值。
   * `switchToLatest` 适合动态选择当前活跃的流，丢弃不活跃流的数据，常用于动态请求或事件流的处理。

这些操作符各自有不同的使用场景和特性，可以根据需求选择最合适的操作符来处理多重流的组合和合并。
