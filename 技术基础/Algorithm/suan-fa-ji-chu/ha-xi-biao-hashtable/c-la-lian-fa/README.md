# C拉链法

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 100

typedef struct KeyValue {
    char *key;
    char *value;
    struct KeyValue *next; // 链表中的下一个元素
} KeyValue;

typedef struct HashTable {
    KeyValue **array; // 指向链表的指针数组
} HashTable;

// 哈希函数
unsigned int hash_function(const char *key) {
    unsigned long hash = 5381;
    int c;

    while ((c = *key++)) {
        hash = ((hash << 5) + hash) + c; // hash * 33 + c
    }

    return hash % TABLE_SIZE;
}

// 创建哈希表
HashTable *create_table() {
    HashTable *table = malloc(sizeof(HashTable));
    table->array = malloc(sizeof(KeyValue *) * TABLE_SIZE);
    
    for (int i = 0; i < TABLE_SIZE; i++) {
        table->array[i] = NULL; // 初始化为 NULL
    }
    
    return table;
}

// 插入元素
void insert(HashTable *table, const char *key, const char *value) {
    unsigned int index = hash_function(key);
    
    KeyValue *new_entry = malloc(sizeof(KeyValue));
    new_entry->key = strdup(key); // 复制键
    new_entry->value = strdup(value); // 复制值
    new_entry->next = table->array[index]; // 新节点指向链表的头
    table->array[index] = new_entry; // 更新链表头
}

// 查找元素
char *find(HashTable *table, const char *key) {
    unsigned int index = hash_function(key);
    KeyValue *current = table->array[index];
    
    while (current != NULL) {
        if (strcmp(current->key, key) == 0) {
            return current->value; // 找到值
        }
        current = current->next; // 继续查找
    }
    
    return NULL; // 未找到
}

// 删除元素
void delete(HashTable *table, const char *key) {
    unsigned int index = hash_function(key);
    KeyValue *current = table->array[index];
    KeyValue *prev = NULL;
    
    while (current != NULL) {
        if (strcmp(current->key, key) == 0) {
            if (prev == NULL) {
                table->array[index] = current->next; // 删除头节点
            } else {
                prev->next = current->next; // 删除中间节点
            }
            free(current->key);
            free(current->value);
            free(current);
            return;
        }
        prev = current;
        current = current->next;
    }
}

// 释放哈希表
void free_table(HashTable *table) {
    for (int i = 0; i < TABLE_SIZE; i++) {
        KeyValue *current = table->array[i];
        while (current != NULL) {
            KeyValue *temp = current;
            current = current->next;
            free(temp->key);
            free(temp->value);
            free(temp);
        }
    }
    free(table->array);
    free(table);
}

// 测试哈希表
int main() {
    HashTable *table = create_table();
    insert(table, "name", "Alice");
    insert(table, "age", "30");

    printf("Name: %s\n", find(table, "name"));
    printf("Age: %s\n", find(table, "age"));

    delete(table, "name");
    printf("Name after deletion: %s\n", find(table, "name"));

    free_table(table);
    return 0;
}
```

#### 说明

* 这个实现使用链表来处理哈希冲突。
* 每个链表节点保存键值对以及指向下一个节点的指针。
* `create_table`、`insert`、`find`、`delete` 和 `free_table` 函数分别实现了创建哈希表、插入、查找、删除和释放哈希表的功能。
