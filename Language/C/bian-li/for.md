---
description: 数组、字符串、或者其他结构中逐步访问每个元素
---

# for



## 索引遍历

```
for (初始化; 条件; 更新) {
    // 循环体
}
```

#### 1. **遍历数组**

```
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
//i 是数组的索引，arr[i] 通过索引访问数组中的元素
```

2、遍历字符串

```
#include <stdio.h>

int main() {
    char str[] = "Hello, World!";

    for (int i = 0; str[i] != '\0'; i++) {
        printf("%c ", str[i]);
    }

    return 0;
}
// str[i] != '\0' 来判断字符串是否结束，因为 C 字符串以空字符 \0 结尾。

```

3、遍历二维

```
#include <stdio.h>

int main() {
    int matrix[2][3] = {{1, 2, 3}, {4, 5, 6}};

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```



{% hint style="info" %}
总结：

C语言中对数组(字符串)的遍历，只有\`索引遍历\`这种方式
{% endhint %}

