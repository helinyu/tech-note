# getenv和setenv

在 C 语言中，`getenv` 和 `setenv` 函数用于处理环境变量。具体如下：

#### 1. `getenv` 函数

`getenv` 函数用于获取指定环境变量的值。其原型如下：

```c
char *getenv(const char *name);
```

* **参数**：`name` 是要获取的环境变量的名称。
* **返回值**：成功时返回环境变量的值的指针；如果找不到该变量，则返回 `NULL`。

**示例**：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char *path = getenv("PATH");
    if (path != NULL) {
        printf("PATH: %s\n", path);
    } else {
        printf("环境变量 PATH 不存在。\n");
    }
    return 0;
}
```

#### 2. `setenv` 函数

`setenv` 函数用于设置或更新环境变量的值。其原型如下：

```c
int setenv(const char *name, const char *value, int overwrite);
```

* **参数**：
  * `name`：环境变量的名称。
  * `value`：要设置的值。
  * `overwrite`：如果为非零且环境变量已存在，则覆盖其值；否则不改变已有值。
* **返回值**：成功时返回 0；若出错（例如内存分配失败）则返回 -1。

**示例**：

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    if (setenv("MY_VAR", "HelloWorld", 1) == 0) {
        printf("MY_VAR 设置成功：%s\n", getenv("MY_VAR"));
    } else {
        perror("设置 MY_VAR 失败");
    }
    return 0;
}
```

#### 注意事项

* 使用 `getenv` 和 `setenv` 操作环境变量时，确保代码的移植性，因为某些操作系统（如 Windows）不支持 `setenv`。
* 在修改环境变量时，需谨慎避免不必要的冲突，尤其是对已有的系统变量的修改。
