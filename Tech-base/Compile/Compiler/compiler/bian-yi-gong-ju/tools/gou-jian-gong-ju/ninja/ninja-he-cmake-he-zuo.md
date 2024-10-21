# ninja 和 cmake合作

以下是一个简单的示例，展示如何将 Ninja 和 CMake 一起使用来构建一个 C++ 项目。

测试[源代码例子地址](https://github.com/hly-code-source/exmaples/tree/main/c%2B%2B/cmake-ninja-test)

#### 1. **项目结构**

假设你的项目目录结构如下：

```
/cmake-ninja-test
  ├── CMakeLists.txt
  ├── main.cpp
```

#### 2. **`main.cpp` 示例**

`main.cpp` 文件包含一个简单的 "Hello, World!" 程序：

```cpp
// main.cpp
#include <iostream>

int main() {
    std::cout << "Hello, Ninja and CMake!" << std::endl;
    return 0;
}
```

#### 3. **`CMakeLists.txt` 文件**

`CMakeLists.txt` 文件是 CMake 的配置文件，它定义了如何编译项目。以下是一个简单的 `CMakeLists.txt`：

```cmake
# 指定 CMake 的最低版本
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(HelloNinja)

# 指定 C++ 标准
set(CMAKE_CXX_STANDARD 11)

# 添加可执行文件
add_executable(hello main.cpp)
```

#### 4. **使用 Ninja 和 CMake 构建项目**

以下步骤展示如何使用 Ninja 和 CMake 一起构建项目：

**步骤 1: 确保安装 Ninja 和 CMake**

首先，需要确保系统上安装了 Ninja 和 CMake。你可以使用以下命令来安装它们：

*   **在 Ubuntu/Linux 上**：

    ```bash
    sudo apt-get install ninja-build cmake
    ```
*   **在 macOS 上**（使用 Homebrew）：

    ```bash
    brew install ninja cmake
    ```

**步骤 2: 使用 CMake 生成 Ninja 构建文件**

在项目的根目录 `/`cmake-ninja-test 下，运行以下命令来生成 Ninja 构建文件：

```bash
cmake -G Ninja .
```

这个命令告诉 CMake 使用 Ninja 生成 `build.ninja` 文件。CMake 将根据 `CMakeLists.txt` 文件生成适用于 Ninja 的构建配置。

**步骤 3: 使用 Ninja 构建项目**

生成 `build.ninja` 文件后，使用 Ninja 来构建项目。运行以下命令：

```bash
ninja
```

Ninja 会读取 `build.ninja` 文件并执行构建过程。你应该会看到以下输出：

```bash
[1/1] Linking CXX executable hello
```

**步骤 4: 运行编译生成的可执行文件**

一旦构建成功，生成的可执行文件（`hello`）将位于项目根目录下。运行它：

```bash
./hello
```

你会看到输出：

```bash
Hello, Ninja and CMake!
```

#### 5. **构建后的目录结构**

构建完成后，项目目录的结构会有所变化，可能会包含以下内容：

```
/cmake-ninja-test
  ├── CMakeLists.txt
  ├── build.ninja   # Ninja 构建文件
  ├── hello         # 可执行文件
  ├── main.cpp
  ├── CMakeCache.txt # CMake 的缓存文件
  ├── CMakeFiles/   # CMake 生成的辅助文件
```

#### 6. **常见操作**

* **重新生成 Ninja 文件**: 如果修改了 `CMakeLists.txt` 文件或源代码，可以再次运行 `cmake -G Ninja .` 以重新生成 Ninja 构建文件。
* **并行构建**: Ninja 默认会利用多核 CPU 进行并行构建，无需手动指定。如果需要控制并行构建的线程数，可以使用 `ninja -j <线程数>`。
* **清理构建文件**: 要清理构建生成的文件，可以运行 `ninja clean`。

#### 总结

通过这个简单的例子，你可以看到 Ninja 和 CMake 一起使用的基本流程。CMake 负责生成 Ninja 所需的构建配置文件，而 Ninja 提供了高效、快速的构建机制，非常适合大型项目的增量构建需求。
