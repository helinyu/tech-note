# While(do..while)

1\. `while` 循环

`while`循环是一种前置条件循环，适合用于不知道具体循环次数但希望在某个条件为`true`时反复执行某些操作的场景。

**语法：**

```c
while (条件) {
    // 循环体
}
```

**示例：遍历数组**

```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int i = 0;
    
    // 使用 while 循环遍历数组
    while (i < 5) {
        printf("%d ", arr[i]);
        i++;
    }
    
    return 0;
}
```

**执行过程：**

1. 检查条件是否为`true`，如果为`true`，则执行循环体，否则退出循环。
2. 循环体执行完后重新检查条件。
3. 重复该过程直到条件为`false`。

#### 2. `do-while` 循环

`do-while`循环是一种后置条件循环，不管条件是否为`true`，循环体至少执行一次。

**语法：**

```c
do {
    // 循环体
} while (条件);
```

**示例：遍历数组**

```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int i = 0;
    
    // 使用 do-while 循环遍历数组
    do {
        printf("%d ", arr[i]);
        i++;
    } while (i < 5);
    
    return 0;
}
```

**执行过程：**

1. 先执行循环体一次。
2. 执行完循环体后，检查条件。如果条件为`true`，则再次执行循环体，否则退出循环。
