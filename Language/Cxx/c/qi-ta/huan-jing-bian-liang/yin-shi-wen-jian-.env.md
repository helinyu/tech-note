# 隐式文件.env

在 C 语言中，标准库并没有内置对 `.env` 文件的支持，通常需要通过手动读取文件来实现类似功能。可以用以下方法在 C 项目中读取 `.env` 文件并设置环境变量。

#### 1. 使用第三方库（如 `libdotenv` 或 `dotenv-c`）

一些第三方库提供了对 `.env` 文件的支持，使得在 C 项目中使用 `.env` 文件更简单。这些库会自动读取 `.env` 文件并将变量添加到当前进程的环境中。示例如下：

```c
#include "dotenv.h" // 假设使用 dotenv-c 库
#include <stdio.h>
#include <stdlib.h>

int main() {
    dotenv_load(); // 加载 .env 文件

    // 使用 getenv 获取 .env 文件中的变量
    const char *myVar = getenv("MY_ENV_VAR");
    if (myVar) {
        printf("MY_ENV_VAR: %s\n", myVar);
    } else {
        printf("未找到 MY_ENV_VAR\n");
    }

    return 0;
}
```

使用此类库可以省去手动读取和解析 `.env` 文件的步骤，特别适合需要频繁使用环境变量的项目。

#### 2. 手动读取 `.env` 文件并设置环境变量

如果不想使用第三方库，可以编写代码手动读取 `.env` 文件，解析每行的 `KEY=VALUE` 格式并设置环境变量。示例代码如下：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void load_env_file(const char *filename) {
    FILE *file = fopen(filename, "r");
    if (!file) {
        perror("无法打开 .env 文件");
        return;
    }

    char line[256];
    while (fgets(line, sizeof(line), file)) {
        // 跳过空行或注释
        if (line[0] == '#' || line[0] == '\n') continue;

        // 找到 '=' 符号的位置并分割成 key 和 value
        char *delimiter = strchr(line, '=');
        if (delimiter) {
            *delimiter = '\0'; // 将 '=' 替换为字符串结束符，分割成 key 和 value
            const char *key = line;
            const char *value = delimiter + 1;

            // 去掉 value 后面的换行符
            value[strcspn(value, "\n")] = '\0';

            // 设置环境变量
            setenv(key, value, 1);
        }
    }

    fclose(file);
}

int main() {
    // 加载 .env 文件
    load_env_file(".env");

    // 获取变量并打印
    const char *myVar = getenv("MY_ENV_VAR");
    if (myVar) {
        printf("MY_ENV_VAR: %s\n", myVar);
    } else {
        printf("未找到 MY_ENV_VAR\n");
    }

    return 0;
}
```

#### 代码说明

1. `load_env_file` 函数打开 `.env` 文件并读取每一行。
2. 检查每行是否包含 `=`，将其分割为键（key）和值（value）。
3. 使用 `setenv` 函数将键值对添加到环境变量中。

#### 注意事项

* 使用 `setenv` 时，将第三个参数设为 `1` 以确保允许覆盖已存在的环境变量。
* `.env` 文件的格式必须为 `KEY=VALUE`，并避免在键和值中使用不必要的空格。
* 如需加载不同的 `.env` 文件，只需修改 `load_env_file` 中传入的文件路径。
