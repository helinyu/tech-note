# cmake 和 ninja

**CMake** 和 **Ninja** 是构建工具链中常常一起使用的两个不同组件，但它们的功能和角色各不相同：

1. **CMake 是构建系统生成器**：
   * CMake 是一种跨平台的构建自动化工具，主要用于生成项目的构建配置文件。CMake 通过读取 `CMakeLists.txt` 中的配置和指令，将项目文件转化为具体构建系统（例如 Ninja、Make、Visual Studio、Xcode 等）可以识别的构建文件。
   * CMake 不直接构建代码，而是生成构建工具的配置文件；换句话说，它只是准备构建过程，而不实际执行编译和链接。
2. **Ninja 是构建系统**：
   * Ninja 是一种轻量、高速的构建系统，专门设计用于处理大型项目的快速增量构建。它擅长在源文件变更后迅速重新构建，只重新编译改动过的部分。
   * Ninja 不能直接使用项目源码进行配置，它需要由 CMake 或其他工具生成的构建文件 (`build.ninja`)。

#### CMake 与 Ninja 的关系：

* 在构建过程中，CMake 通常用于解析配置并生成 Ninja 所需的 `build.ninja` 文件，随后 Ninja 通过这个文件构建项目。
* CMake 本身并不强制使用 Ninja，用户也可以选择生成 Makefile 或其他构建系统的配置文件。但是，Ninja 常常与 CMake 搭配使用，因为其构建速度较快且依赖分析精确，特别适合大型项目的快速编译。

#### CMake 与 Ninja 的区别：

* **角色**：CMake 是生成器，Ninja 是执行器。
* **目的**：CMake 用于配置项目并生成构建文件；Ninja 用于根据生成的文件高效地构建项目。
