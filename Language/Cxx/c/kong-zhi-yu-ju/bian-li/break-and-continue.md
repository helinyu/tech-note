# break & continue

#### 4. `break` 和 `continue` 关键字

* **`break`**：用于立即跳出循环，不再继续执行。
* **`continue`**：用于跳过当前循环体的剩余部分，直接进入下一次迭代。

**示例：使用 `break` 跳出循环**

```c
#include <stdio.h>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break;  // 当 i 等于 5 时跳出循环
        }
        printf("%d ", i);
    }
    return 0;
}
```

**示例：使用 `continue` 跳过迭代**

```c
#include <stdio.h>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue;  // 如果 i 是偶数，跳过本次循环
        }
        printf("%d ", i);
    }
    return 0;
}
```
