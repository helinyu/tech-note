# OC你了解的锁有哪些？

在 Objective-C 中，有多种锁机制可用于实现线程安全，确保多个线程在访问共享资源时不会出现数据竞争或不一致的情况。以下是一些常见的锁类型及其特点：

#### 1. **NSLock**

* **描述**：`NSLock` 是一种基本的互斥锁，提供简单的加锁和解锁方法。
*   **使用示例**：

    ```objc
    NSLock *lock = [[NSLock alloc] init];

    [lock lock];
    // 访问共享资源
    [lock unlock];
    ```

#### 2. **NSRecursiveLock**

* **描述**：`NSRecursiveLock` 是一种可重入锁，允许同一线程多次获得锁而不会导致死锁。
* **使用场景**：适用于在同一线程中调用需要锁保护的多个方法。
*   **使用示例**：

    ```objc
    NSRecursiveLock *recursiveLock = [[NSRecursiveLock alloc] init];

    [recursiveLock lock];
    // 可以再次加锁
    [recursiveLock lock];
    // 访问共享资源
    [recursiveLock unlock];
    [recursiveLock unlock]; // 必须调用两次 unlock
    ```

#### 3. **@synchronized**

* **描述**：`@synchronized` 是一种简化的语法，用于在代码块中自动加锁和解锁。它会为每个对象创建一个锁，适用于快速实现线程安全。
*   **使用示例**：

    ```objc
    @synchronized(self) {
        // 访问共享资源
    }
    ```

#### 4. **Dispatch Semaphore (信号量)**

* **描述**：使用信号量控制对共享资源的访问，允许一定数量的线程同时访问。
*   **使用示例**：

    ```objc
    dispatch_semaphore_t semaphore = dispatch_semaphore_create(1);

    dispatch_semaphore_wait(semaphore, DISPATCH_TIME_FOREVER);
    // 访问共享资源
    dispatch_semaphore_signal(semaphore);
    ```

#### 5. **NSCondition**

* **描述**：`NSCondition` 用于在多线程中实现条件变量，允许线程在满足特定条件时进行等待和唤醒。
*   **使用示例**：

    ```objc
    NSCondition *condition = [[NSCondition alloc] init];

    [condition lock];
    while (!conditionMet) {
        [condition wait]; // 等待条件满足
    }
    // 访问共享资源
    [condition unlock];
    ```

#### 6. **NSConditionLock**

* **描述**：`NSConditionLock` 是 `NSCondition` 的扩展，结合了条件变量和锁的特性，可以在满足特定条件时进行加锁和解锁。
*   **使用示例**：

    ```objc
    NSConditionLock *conditionLock = [[NSConditionLock alloc] initWithCondition:0];

    [conditionLock lockWhenCondition:1];
    // 访问共享资源
    [conditionLock unlockWithCondition:0]; // 更新条件
    ```

#### 7. **OS\_UNFAIR\_LOCK**

* **描述**：自 iOS 10 和 macOS 10.12 起引入的锁，性能比 `NSLock` 更高，但不支持重入。
*   **使用示例**：

    ```objc
    os_unfair_lock lock = OS_UNFAIR_LOCK_INIT;

    os_unfair_lock_lock(&lock);
    // 访问共享资源
    os_unfair_lock_unlock(&lock);
    ```

#### 总结

选择合适的锁类型取决于具体的需求和场景。对于简单的互斥访问，`NSLock` 或 `@synchronized` 可能足够；而对于更复杂的需求，可能需要使用 `NSRecursiveLock`、`NSCondition` 或信号量等机制。确保在使用锁时避免死锁和性能瓶颈是至关重要的。
