# SDWebImage中的clear和clean有什么样的区别

在 SDWebImage 中，`clear` 和 `clean` 两个术语通常与缓存管理相关，但它们的使用和意义有些不同。以下是它们的主要区别：

#### 1. **clear**

* **功能**：`clear` 通常指的是清理缓存中的所有条目，包括内存和磁盘缓存。调用 `clearMemory` 或 `clearDisk` 方法会立即删除缓存中的所有图像。
*   **用法**：

    * `clearMemory`：清除内存中的所有图像缓存。
    * `clearDiskOnCompletion:`：清除磁盘中的所有图像缓存，并在完成后执行指定的操作。

    示例：

    ```objc
    [[SDImageCache sharedImageCache] clearMemory]; // 清理内存缓存
    [[SDImageCache sharedImageCache] clearDiskOnCompletion:^{
        NSLog(@"Disk cache cleared.");
    }]; // 清理磁盘缓存
    ```

#### 2. **clean**

* **功能**：`clean` 通常不是 SDWebImage API 中的直接调用，而是一个更一般的概念，指的是定期清理过期的缓存条目或执行优化操作，以保持缓存的健康状态。
* **示例**：虽然 SDWebImage 没有直接提供 `clean` 方法，但它会在使用过程中自动处理缓存的清理，比如删除过期的缓存。

#### 总结

* **`clear`** 是明确的清理操作，立即移除缓存内容。
* **`clean`** 是一种更通用的概念，通常与维护和优化缓存相关，可能涉及自动管理和定期清理。

在 SDWebImage 的实际使用中，通常会看到 `clear` 方法，但在缓存管理的上下文中，`clean` 可以理解为一种策略或过程。
