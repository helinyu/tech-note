# 用C/OC/C++，任选其一，实现自旋或互斥？

下面我将提供一个用 **C** 语言实现自旋锁和互斥锁的简单示例。

#### 1. 自旋锁（Spin Lock）

```c
#include <stdio.h>
#include <pthread.h>
#include <stdatomic.h>
#include <unistd.h>

typedef struct {
    atomic_flag lock; // 使用原子标志表示锁的状态
} SpinLock;

// 初始化自旋锁
void spinlock_init(SpinLock* s) {
    atomic_flag_clear(&s->lock);
}

// 获取自旋锁
void spinlock_lock(SpinLock* s) {
    while (atomic_flag_test_and_set(&s->lock)) {
        // 自旋等待
    }
}

// 释放自旋锁
void spinlock_unlock(SpinLock* s) {
    atomic_flag_clear(&s->lock);
}

SpinLock spinlock;

void* thread_function(void* arg) {
    // 尝试获取自旋锁
    spinlock_lock(&spinlock);
    printf("Thread %ld acquired the spin lock.\n", (long)arg);
    sleep(1); // 模拟工作
    printf("Thread %ld releasing the spin lock.\n", (long)arg);
    spinlock_unlock(&spinlock);
    return NULL;
}

int main() {
    pthread_t threads[5];
    spinlock_init(&spinlock);

    // 创建多个线程
    for (long i = 0; i < 5; i++) {
        pthread_create(&threads[i], NULL, thread_function, (void*)i);
    }

    // 等待线程完成
    for (int i = 0; i < 5; i++) {
        pthread_join(threads[i], NULL);
    }

    return 0;
}
```

#### 2. 互斥锁（Mutex Lock）

```c
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t mutex;

void* thread_function(void* arg) {
    // 尝试获取互斥锁
    pthread_mutex_lock(&mutex);
    printf("Thread %ld acquired the mutex lock.\n", (long)arg);
    sleep(1); // 模拟工作
    printf("Thread %ld releasing the mutex lock.\n", (long)arg);
    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main() {
    pthread_t threads[5];
    pthread_mutex_init(&mutex, NULL); // 初始化互斥锁

    // 创建多个线程
    for (long i = 0; i < 5; i++) {
        pthread_create(&threads[i], NULL, thread_function, (void*)i);
    }

    // 等待线程完成
    for (int i = 0; i < 5; i++) {
        pthread_join(threads[i], NULL);
    }

    pthread_mutex_destroy(&mutex); // 销毁互斥锁
    return 0;
}
```

#### 说明

* **自旋锁**：使用 `atomic_flag` 实现自旋锁，线程在获取锁时自旋等待，直到锁可用。自旋锁适用于锁持有时间短且线程数量较少的情况。
* **互斥锁**：使用 `pthread_mutex_t` 实现互斥锁，线程在请求锁时会被挂起，适用于锁持有时间较长的情况。

#### 编译与运行

可以使用 GCC 编译这些示例：

```bash
gcc -o spinlock_example spinlock_example.c -lpthread
./spinlock_example

gcc -o mutex_example mutex_example.c -lpthread
./mutex_example
```

根据你的需求选择自旋锁或互斥锁，并注意它们各自的适用场景和性能特点。
