# set的实现

下面是一个使用线性探测法实现的哈希表（set）数据结构的 C 语言示例。

这个实现允许插入、查找和删除元素，并支持扩容和缩小。

```c
#include <stdio.h>
#include <stdlib.h>

#define INITIAL_SIZE 10
#define LOAD_FACTOR 0.7

typedef struct {
    int key;
    int occupied; // 标记该位置是否被占用
} HashEntry;

typedef struct {
    HashEntry *table;
    int size;  // 当前表的大小
    int count; // 当前元素的数量
} HashSet;

// 创建哈希集合
HashSet* create_set(int initial_size) {
    HashSet *set = malloc(sizeof(HashSet));
    set->size = initial_size;
    set->count = 0;
    set->table = malloc(sizeof(HashEntry) * initial_size);
    for (int i = 0; i < initial_size; i++) {
        set->table[i].occupied = 0; // 初始化为未占用
    }
    return set;
}

// 哈希函数
int hash(int key, int size) {
    return key % size;
}

// 重新哈希
void rehash(HashSet *set, int new_size) {
    HashEntry *old_table = set->table;
    int old_size = set->size;

    set->table = malloc(sizeof(HashEntry) * new_size);
    for (int i = 0; i < new_size; i++) {
        set->table[i].occupied = 0; // 初始化为未占用
    }
    set->size = new_size;
    set->count = 0;

    for (int i = 0; i < old_size; i++) {
        if (old_table[i].occupied) {
            // 重新插入
            insert(set, old_table[i].key);
        }
    }
    free(old_table);
}

// 插入元素
void insert(HashSet *set, int key) {
    if ((float)set->count / set->size >= LOAD_FACTOR) {
        rehash(set, set->size * 2); // 扩容
    }

    int index = hash(key, set->size);
    while (set->table[index].occupied) {
        if (set->table[index].key == key) {
            return; // 元素已存在
        }
        index = (index + 1) % set->size; // 线性探测
    }
    set->table[index].key = key;
    set->table[index].occupied = 1; // 标记为已占用
    set->count++;
}

// 查找元素
int search(HashSet *set, int key) {
    int index = hash(key, set->size);
    while (set->table[index].occupied) {
        if (set->table[index].key == key) {
            return 1; // 找到元素
        }
        index = (index + 1) % set->size; // 线性探测
    }
    return 0; // 未找到元素
}

// 删除元素
void remove_element(HashSet *set, int key) {
    int index = hash(key, set->size);
    while (set->table[index].occupied) {
        if (set->table[index].key == key) {
            set->table[index].occupied = 0; // 标记为未占用
            set->count--;
            if ((float)set->count / set->size < LOAD_FACTOR / 4) {
                rehash(set, set->size / 2); // 缩小
            }
            return;
        }
        index = (index + 1) % set->size; // 线性探测
    }
}

// 销毁哈希集合
void free_set(HashSet *set) {
    free(set->table);
    free(set);
}

int main() {
    HashSet *set = create_set(INITIAL_SIZE);
    
    insert(set, 1);
    insert(set, 2);
    insert(set, 3);
    insert(set, 11); // 这将与键 1 冲突

    printf("Search for 1: %d\n", search(set, 1));
    printf("Search for 2: %d\n", search(set, 2));
    printf("Search for 11: %d\n", search(set, 11));
    printf("Search for 4: %d\n", search(set, 4)); // 未插入

    remove_element(set, 1);
    printf("Search for 1 after deletion: %d\n", search(set, 1));

    free_set(set);
    return 0;
}
```

#### 代码说明：

1. **结构体定义**：
   * `HashEntry`：存储键和占用状态。
   * `HashSet`：包含哈希表、大小和元素数量。
2. **哈希函数**：根据键对表的大小取模，计算索引。
3. **插入**：如果元素已存在，则不插入；使用线性探测解决冲突。
4. **查找**：遍历表，通过线性探测查找元素。
5. **删除**：标记元素为未占用，如果负载因子过低，则进行缩小。
6. **内存管理**：使用 `free_set` 函数释放内存。

这个实现提供了基本的集合功能，可以根据需要进行扩展或修改。
