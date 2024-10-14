# Windows

在 Windows 中，获取和设置环境变量的主要函数有 `GetEnvironmentVariable` 和 `SetEnvironmentVariable`。以下是这些函数的详细介绍及示例代码：

#### 1. `GetEnvironmentVariable` 函数

`GetEnvironmentVariable` 函数用于获取指定环境变量的值。

**原型**

```c
DWORD GetEnvironmentVariable(
  LPCSTR lpName,
  LPSTR lpValue,
  DWORD nSize
);
```

* **参数**：
  * `lpName`：要获取的环境变量的名称。
  * `lpValue`：用于接收环境变量值的缓冲区。
  * `nSize`：缓冲区的大小，以字符为单位。
* **返回值**：成功时返回环境变量的长度（以字符为单位）；如果缓冲区不足以存放值，则返回所需的字符数；出错时返回 0。

**示例**

```c
#include <windows.h>
#include <stdio.h>

int main() {
    char value[1024];
    DWORD length = GetEnvironmentVariable("PATH", value, sizeof(value));

    if (length > 0 && length < sizeof(value)) {
        printf("PATH: %s\n", value);
    } else if (length == 0) {
        printf("获取环境变量失败。\n");
    } else {
        printf("缓冲区不足，需要 %lu 个字符。\n", length);
    }

    return 0;
}
```

#### 2. `SetEnvironmentVariable` 函数

`SetEnvironmentVariable` 函数用于设置或更新环境变量的值。

**原型**

```c
BOOL SetEnvironmentVariable(
  LPCSTR lpName,
  LPCSTR lpValue
);
```

* **参数**：
  * `lpName`：要设置的环境变量的名称。
  * `lpValue`：要设置的值；如果值为 `NULL`，则删除该环境变量。
* **返回值**：成功时返回非零值；失败时返回 0。

**示例**

```c
#include <windows.h>
#include <stdio.h>

int main() {
    if (SetEnvironmentVariable("MY_VAR", "HelloWorld")) {
        printf("MY_VAR 设置成功\n");
    } else {
        printf("设置 MY_VAR 失败\n");
    }

    // 验证 MY_VAR 是否被设置
    char value[1024];
    DWORD length = GetEnvironmentVariable("MY_VAR", value, sizeof(value));
    if (length > 0) {
        printf("MY_VAR: %s\n", value);
    } else {
        printf("环境变量 MY_VAR 不存在。\n");
    }

    return 0;
}
```

#### 注意事项

* `SetEnvironmentVariable` 只会影响当前进程的环境变量，若希望对系统或用户级的环境变量做持久修改，可以通过控制面板或注册表等方式。
* 在使用 `GetEnvironmentVariable` 时，确保提供足够大的缓冲区来存放环境变量的值。
