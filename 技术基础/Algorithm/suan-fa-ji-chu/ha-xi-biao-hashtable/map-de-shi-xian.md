# map的实现

下面是一个使用线性探测法实现的哈希表（map）数据结构的 C 语言示例。

该实现允许插入、查找和删除键值对，并支持扩容和缩小。

{% code overflow="wrap" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define INITIAL_SIZE 10
#define LOAD_FACTOR 0.7

typedef struct {
    int key;         // 整数键
    int value;       // 整数值
    int occupied;    // 标记该位置是否被占用
} HashEntry;
// 注意，结构里面都是存有原来需要的数据，
//不管是key/value或者是一个复杂的对象，都是要存在hashEntry这样的结构里面

typedef struct {
    HashEntry *table; // 哈希表
    int size;         // 当前表的大小
    int count;        // 当前元素的数量
} HashMap;


// 创建哈希表
HashMap* create_map(int initial_size) {
    HashMap *map = malloc(sizeof(HashMap));
    map->size = initial_size;
    map->count = 0;
    map->table = malloc(sizeof(HashEntry) * initial_size);
    for (int i = 0; i < initial_size; i++) {
        map->table[i].occupied = 0; // 初始化为未占用
    }
    return map;
}

// 哈希函数
int hash(int key, int size) {
    return key % size;
}

// 重新哈希
void rehash(HashMap *map, int new_size) {
    HashEntry *old_table = map->table;
    int old_size = map->size;

    map->table = malloc(sizeof(HashEntry) * new_size);
    for (int i = 0; i < new_size; i++) {
        map->table[i].occupied = 0; // 初始化为未占用
    }
    map->size = new_size;
    map->count = 0;

    for (int i = 0; i < old_size; i++) {
        if (old_table[i].occupied) {
            // 重新插入
            insert(map, old_table[i].key, old_table[i].value);
        }
    }
    free(old_table);
}

// 插入键值对
void insert(HashMap *map, int key, int value) {
    if ((float)map->count / map->size >= LOAD_FACTOR) {
        rehash(map, map->size * 2); // 扩容
    }

    int index = hash(key, map->size);
    while (map->table[index].occupied) {
        if (map->table[index].key == key) {
            map->table[index].value = value; // 更新值
            return;
        }
        index = (index + 1) % map->size; // 线性探测
    }
    map->table[index].key = key;
    map->table[index].value = value;
    map->table[index].occupied = 1; // 标记为已占用
    map->count++;
}

// 查找值
int search(HashMap *map, int key) {
    int index = hash(key, map->size);
    while (map->table[index].occupied) {
        if (map->table[index].key == key) {
            return map->table[index].value; // 找到值
        }
        index = (index + 1) % map->size; // 线性探测
    }
    return -1; // 未找到
}

// 删除键值对
void remove_element(HashMap *map, int key) {
    int index = hash(key, map->size);
    while (map->table[index].occupied) {
        if (map->table[index].key == key) {
            map->table[index].occupied = 0; // 标记为未占用
            map->count--;
            if ((float)map->count / map->size < LOAD_FACTOR / 4) {
                rehash(map, map->size / 2); // 缩小
            }
            return;
        }
        index = (index + 1) % map->size; // 线性探测
    }
}

// 销毁哈希表
void free_map(HashMap *map) {
    free(map->table);
    free(map);
}

int main() {
    HashMap *map = create_map(INITIAL_SIZE);
    
    insert(map, 1, 100);
    insert(map, 2, 200);
    insert(map, 11, 300); // 这将与键 1 冲突

    printf("Value for key 1: %d\n", search(map, 1));
    printf("Value for key 2: %d\n", search(map, 2));
    printf("Value for key 11: %d\n", search(map, 11));
    printf("Value for key 3 (not present): %d\n", search(map, 3)); // 未插入

    remove_element(map, 1);
    printf("Value for key 1 after deletion: %d\n", search(map, 1));

    free_map(map);
    return 0;
}
```
{% endcode %}

#### 代码说明：

1. **结构体定义**：
   * `HashEntry`：存储键、值和占用标志。
   * `HashMap`：包含哈希表、大小和元素数量。
2. **哈希函数**：根据键对表的大小取模，计算索引。
3. **插入**：如果键已存在，则更新其值；使用线性探测解决冲突。
4. **查找**：遍历表，通过线性探测查找键对应的值。
5. **删除**：标记元素为未占用，如果负载因子过低，则进行缩小。
6. **内存管理**：使用 `free_map` 函数释放分配的内存。

这个实现提供了基本的映射功能，可以根据需要进行扩展或修改，例如支持字符串键、不同类型的值等。
