# SDWebImage是怎么清理缓存的？

SDWebImage 提供了多种方式来清理缓存，包括以下几种常见的方法：

#### 1. **清理内存缓存**

* SDWebImage 在内存中缓存图像数据，可以通过调用 `SDImageCache` 的 `clearMemory` 方法来清理内存缓存。这个方法会立即释放内存中存储的所有图像。

#### 2. **清理磁盘缓存**

* SDWebImage 也将图像数据缓存到磁盘上，可以使用 `clearDisk` 方法来清理磁盘缓存。这个方法会异步执行，并释放磁盘上存储的所有图像文件。

#### 3. **清理过期缓存**

* 通过设置缓存的最大过期时间，SDWebImage 会在加载图像时自动检查并清理过期的缓存。可以通过 `maxCacheAge` 属性来设置最大缓存时间。

#### 4. **根据特定条件清理**

* 还可以使用 `removeImageForKey:fromDisk:` 方法删除特定的缓存图像，或者根据条件清理特定的缓存。

#### 5. **使用 Cache Control 头**

* 在 HTTP 请求中使用 Cache Control 头可以指示 SDWebImage 如何处理缓存，比如通过设置 `no-cache` 或 `max-age` 来控制缓存的行为。

通过这些方法，开发者可以灵活管理和清理 SDWebImage 的缓存，以优化应用的性能和内存使用。如果需要了解更详细的代码示例或实现，可以告诉我！
