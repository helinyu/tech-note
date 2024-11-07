# 多线程

| **多线程机制**                          | **描述**                                   | **优点**                                      | **缺点**                                     |
| ---------------------------------- | ---------------------------------------- | ------------------------------------------- | ------------------------------------------ |
| **GCD (Grand Central Dispatch)**   | 提供了简单的方式来执行并发任务，支持全局和自定义队列。              | <p>- 简单易用<br>- 高效管理并发任务<br>- 自动处理线程池</p>    | <p>- 难以处理任务依赖<br>- 代码可读性较差</p>             |
| **NSOperation / NSOperationQueue** | 提供更高级的任务管理，支持任务依赖、优先级和取消。                | <p>- 可配置性强<br>- 支持依赖关系<br>- 提供任务状态监控</p>    | <p>- 相对 GCD 更复杂<br>- 性能稍差于 GCD</p>         |
| **Thread**                         | 直接创建和管理线程的类，允许更低级的控制。                    | <p>- 完全控制线程的生命周期<br>- 适合对线程有特定需求的场景</p>     | <p>- 复杂性高<br>- 资源管理困难，容易引发竞争条件</p>         |
| **Swift Concurrency**              | 新的并发模型，使用 `async` 和 `await` 关键字，支持结构化并发。 | <p>- 代码更加清晰<br>- 易于处理异步任务<br>- 自动处理线程调度</p> | <p>- 仅支持 iOS 15 及以上版本<br>- 需要理解新的概念和语法</p> |

#### 适用场景

* **GCD**: 简单的并发任务，尤其是无需复杂依赖关系时。
* **NSOperation**: 需要管理复杂依赖关系或任务状态时。
* **Thread**: 需要低级控制的特定场景，但一般不推荐。
* **Swift Concurrency**: 需要更现代化和简洁的代码时，适合处理大量异步操作。



<figure><img src="../../../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

### 线程的同步方案

<figure><img src="../../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

### 读写安全

<figure><img src="../../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>
