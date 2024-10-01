# 线性探测

下面是一个使用线性探测法解决冲突的哈希表实现，支持扩容和缩小功能。

这个实现包含插入、查找、删除、扩容和缩小操作。

```c
#include <stdio.h>
#include <stdlib.h>

#define INITIAL_TABLE_SIZE 10
#define LOAD_FACTOR 0.7


typedef struct {
    int key;
    int value;
    int occupied; // 用于标记该位置是否被占用
} HashEntry;

typedef struct {
    HashEntry *table;
    int size; // 当前表的大小
    int count; // 当前键值对的数量
} HashTable;

// 创建哈希表
HashTable* create_table(int size) {
    HashTable *ht = malloc(sizeof(HashTable));
    ht->size = size;
    ht->count = 0;
    ht->table = malloc(sizeof(HashEntry) * size);
    for (int i = 0; i < size; i++) {
        ht->table[i].occupied = 0; // 初始化为未占用
    }
    return ht;
}

void insert(HashTable *ht, int key, int value);

// 哈希函数
int hash(int key, int size) {
    return key % size;
}

// 重新哈希
void rehash(HashTable *ht, int new_size) {
    HashEntry *old_table = ht->table;
    int old_size = ht->size;

    ht->table = malloc(sizeof(HashEntry) * new_size);
    for (int i = 0; i < new_size; i++) {
        ht->table[i].occupied = 0; // 初始化为未占用
    }
    ht->size = new_size;
    ht->count = 0;

    for (int i = 0; i < old_size; i++) {
        if (old_table[i].occupied) {
            // 重新插入
            insert(ht, old_table[i].key, old_table[i].value);
        }
    }
    free(old_table);
}

// 插入键值对
void insert(HashTable *ht, int key, int value) {
    if ((float)ht->count / ht->size >= LOAD_FACTOR) {
        rehash(ht, ht->size * 2); // 扩容
    }

    int index = hash(key, ht->size);
    while (ht->table[index].occupied) {
        index = (index + 1) % ht->size; // 线性探测
    }
    ht->table[index].key = key;
    ht->table[index].value = value;
    ht->table[index].occupied = 1; // 标记为已占用
    ht->count++;
}

// 查找值
// 查找退出条件：
// 没找到： 没有被占用0==false
// 找到：向上遍历，如果是已经占用occupied==true，并且key相等,即为找到
//  如果key不相等，就继续往下找，找到有occupied==false的时候退出
// 这里有一个问题，如果我的列表都为occupied==true，那么岂不是循环？
// 因为我们有一个负载因子，一般是远小于1的。所以，不可能占满列表
int search(HashTable *ht, int key) {
    int index = hash(key, ht->size);
    while (ht->table[index].occupied) {
        if (ht->table[index].key == key) {
            return ht->table[index].value;
        }
        index = (index + 1) % ht->size; // 线性探测
    }
    return -1; // 未找到
}

// 删除键值对
void delete(HashTable *ht, int key) {
    int index = hash(key, ht->size);
    while (ht->table[index].occupied) {
        if (ht->table[index].key == key) {
            ht->table[index].occupied = 0; // 标记为未占用
            ht->count--;
            if ((float)ht->count / ht->size < LOAD_FACTOR / 4) {
                rehash(ht, ht->size / 2); // 缩小
            }
            return;
        }
        index = (index + 1) % ht->size; // 线性探测
    }
}

// 销毁哈希表
void free_table(HashTable *ht) {
    free(ht->table);
    free(ht);
}

int main(void) {
    HashTable *ht = create_table(INITIAL_TABLE_SIZE);
    
    insert(ht, 1, 10);
    insert(ht, 2, 20);
    insert(ht, 11, 30); // 这将与键 1 冲突

    printf("Value for key 1: %d\n", search(ht, 1));
    printf("Value for key 2: %d\n", search(ht, 2));
    printf("Value for key 11: %d\n", search(ht, 11));

    delete(ht, 1);
    printf("Value for key 1 after deletion: %d\n", search(ht, 1));

    delete(ht, 2);
    delete(ht, 11);
    printf("Value for key 2 after deletion: %d\n", search(ht, 2));

    free_table(ht);
    return 0;
}
```

#### 代码说明：

1. **哈希表结构**：包含一个 `HashEntry` 数组，表的当前大小和键值对的数量。
2. **哈希函数**：根据表的大小计算哈希值。
3. **重新哈希**：在扩容和缩小时，重新分配内存并插入已有的键值对。
4. **扩容与缩小**：在插入时，如果当前负载因子超过阈值，进行扩容；在删除时，如果负载因子低于某个阈值，则进行缩小。
5. **内存管理**：`free_table` 函数用于释放分配的内存。

这个实现是一个基础的哈希表，可以根据需要进行扩展和改进，比如支持更多的数据类型、处理删除时的重排等。



{% hint style="info" %}
这里设置负载因子很重要，永远都是小于的1，负载因子影响着哈希表的增大和缩小。
{% endhint %}



***

[iOS的runtime实现的DenseMap](https://hly-tech.gitbook.io/front-end/ios/xiang-guan-yuan-ma-yue-du/objc4/chou-mi-ha-xi-biao-densemapdenseset)
