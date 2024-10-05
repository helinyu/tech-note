# 内存管理函数

在 C 语言中，常用的内存分配方法有以下几种：

定义在 `<stdlib.h>` 头文件中，用于手动管理内存。

1. **`malloc` (Memory Allocation)**
   * 功能：动态分配一块指定大小的内存，返回一个指向这块内存的指针。
   * 语法：`void* malloc(size_t size);`
   * 返回值：成功时返回一个指向分配内存的指针，失败时返回 `NULL`。
   *   例子：

       ```c
       int *arr = (int*) malloc(10 * sizeof(int)); // 分配存储 10 个整数的空间
       ```
2. **`calloc` (Contiguous Allocation)**
   * 功能：分配指定数量的内存块，并初始化为 0。
   * 语法：`void* calloc(size_t num, size_t size);`
   * 返回值：成功时返回指向分配内存的指针，失败时返回 `NULL`。
   *   例子：

       ```c
       int *arr = (int*) calloc(10, sizeof(int)); // 分配存储 10 个整数的空间并初始化为 0
       ```
3. **`realloc` (Reallocation)**
   * 功能：重新调整已分配内存的大小，可能会移动内存块到新的位置。
   * 语法：`void* realloc(void *ptr, size_t new_size);`
   * 返回值：成功时返回指向新分配内存的指针，失败时返回 `NULL`，原内存不变。
   *   例子：

       ```c
       arr = (int*) realloc(arr, 20 * sizeof(int)); // 将原内存调整为存储 20 个整数的大小
       ```
4. **`free`**
   * 功能：释放由 `malloc`、`calloc` 或 `realloc` 分配的内存，避免内存泄漏。
   * 语法：`void free(void *ptr);`
   *   例子：

       ```c
       free(arr); // 释放分配的内存
       ```



<table data-header-hidden><thead><tr><th width="122"></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>维度</strong></td><td><strong><code>malloc</code></strong></td><td><strong><code>calloc</code></strong></td><td><strong><code>realloc</code></strong></td><td><strong><code>free</code></strong></td></tr><tr><td><strong>主要功能</strong></td><td>分配指定大小的内存</td><td>分配指定数量的内存块并初始化为 0</td><td>重新调整已分配内存的大小</td><td>释放动态分配的内存</td></tr><tr><td><strong>初始化</strong></td><td>未初始化</td><td>初始化为 0</td><td>不会初始化新增加的部分</td><td>无</td></tr><tr><td><strong>语法</strong></td><td><code>void* malloc(size_t size)</code></td><td><code>void* calloc(size_t num, size_t size)</code></td><td><code>void* realloc(void* ptr, size_t size)</code></td><td><code>void free(void* ptr)</code></td></tr><tr><td><strong>返回值</strong></td><td>成功返回内存地址，失败返回 <code>NULL</code></td><td>成功返回内存地址，失败返回 <code>NULL</code></td><td>成功返回新内存地址，失败返回 <code>NULL</code></td><td>无返回值</td></tr><tr><td><strong>内存调整</strong></td><td>不支持</td><td>不支持</td><td>支持</td><td>不适用</td></tr><tr><td><strong>使用场景</strong></td><td>适合需要动态分配未初始化内存的场景</td><td>适合需要初始化为 0 的内存块的场景</td><td>适合需要调整动态内存大小的场景</td><td>释放 <code>malloc</code>、<code>calloc</code>、<code>realloc</code> 分配的内存</td></tr><tr><td><strong>性能</strong></td><td>分配速度较快，但需手动初始化</td><td>较 <code>malloc</code> 稍慢，因为需要初始化</td><td>速度取决于是否需要移动内存</td><td>无</td></tr><tr><td><strong>内存碎片问题</strong></td><td>可能造成内存碎片</td><td>可能造成内存碎片</td><td>可能引入或减少内存碎片</td><td>无</td></tr><tr><td><strong>适用范围</strong></td><td>任意类型的数据块</td><td>初始化后的数据块，适合清零需求的场景</td><td>调整大小的内存块</td><td>任意动态内存</td></tr></tbody></table>

#### 详细解释：

* **`malloc`**: 用于动态分配未初始化的内存，速度较快，但需手动初始化，灵活度较高。
* **`calloc`**: 适合需要分配后立即使用且希望内存初始化为 0 的场景，稍慢于 `malloc`。
* **`realloc`**: 用于调整已经分配内存的大小，适合需要动态调整内存空间的情况，但可能导致内存位置移动。
* **`free`**: 用于释放由 `malloc`、`calloc`、`realloc` 分配的内存，防止内存泄漏。
