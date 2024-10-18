# 构建工具

构建系统生成工具主要是用于生成构建配置和项目结构的工具，而不是实际执行构建的工具。以下是一些常见的构建系统生成工具，排除构建工具本身：

1. <mark style="color:red;">**CMake**</mark>: 生成Makefile、Ninja文件或其他构建系统的配置文件。
2. <mark style="color:red;">**Bazel**</mark>: 提供了一种描述构建过程的语言，可以生成构建配置。
3. **Gradle**: 通过DSL描述项目结构和依赖关系，生成构建配置。
4. **Meson**: 使用简单的配置文件生成构建说明，适合快速构建和开发。
5. **Premake**: 用Lua语言编写的项目生成器，可以生成Makefile、Visual Studio解决方案等。
6. **Qbs**: 一个跨平台的构建系统，支持生成各种构建配置，专注于项目描述。
7. **SCons**: 虽然是一个构建工具，但其使用Python脚本描述项目结构和依赖关系，也可以视为一种生成工具。
8. **Kobalt**: 以Kotlin编写的构建工具，强调简化的构建描述和生成。
9. **CMake Presets**: CMake的新功能，可以在项目中定义不同的构建选项和环境配置，以便快速生成构建配置。
10. **Buck**: 由Facebook开发的构建工具，使用自定义的DSL描述构建配置，支持多种语言，能够快速生成构建配置。
11. **CMake GUI**: 作为CMake的一部分，提供图形用户界面（GUI）来生成构建系统配置，适合不熟悉命令行的用户。
12. **Visual Studio Project System**: 用于生成Visual Studio项目文件，支持多种项目类型和语言。
13. **OpenBuildService**: 用于生成和维护软件包的构建工具，特别是在Linux环境中，用于生成多个发行版的软件包。
14. **Ninja's generator**: 尽管Ninja是一个构建工具，但它通常与其他生成工具结合使用，作为构建过程的最终生成器。
15. **CMake for iOS**: 专门针对iOS项目的CMake配置，自动生成Xcode项目文件。
16. **FPM (Effing Package Management)**: 用于创建软件包的工具，能够生成特定于平台的包文件。
17. **Ant**: 尽管是一个构建工具，但它提供了生成XML构建文件的功能，适合Java项目。
18. **Buildroot**: 生成嵌入式Linux系统的工具，负责生成根文件系统、内核和用户空间的构建配置。
19. **Cargo**: Rust的构建系统和包管理器，可以生成Cargo.toml配置文件，管理Rust项目的依赖和构建。
20. **Lerna**: 用于管理JavaScript项目的工具，特别是包含多个包的monorepo，生成相关的构建配置。

当然，以下是更多的构建系统生成工具，排除执行实际构建的工具：

21. **Yocto Project**: 一个用于生成嵌入式Linux系统的自动化工具链，它负责生成整个系统的构建配置，适用于嵌入式设备开发。
22. **Autotools (GNU Build System)**: 包含`autoconf`、`automake`等工具，用于生成跨平台的构建配置文件，尤其是在Unix-like系统上很常用。
23. **GYP (Generate Your Projects)**: 由Chromium项目开发，用于生成跨平台的项目构建文件，支持生成Makefile、Visual Studio、Xcode项目等。
24. **Cereal**: 类似于Premake，Cereal是一种基于YAML的构建配置生成工具，支持生成项目的构建文件。
25. **XcodeGen**: 一个开源工具，用于根据YAML或JSON文件自动生成Xcode项目文件，这对于iOS和macOS开发非常有用。
26. **Pants**: 一个面向多语言、多项目代码库的构建生成工具，常用于大规模的monorepo。
27. **SLAM**: 一个专注于自动生成低层次构建系统配置的工具，主要用于硬件设计和仿真领域。
28. **GN (Generate Ninja)**: 由Chromium项目开发，生成Ninja文件作为其主要的构建文件格式。GN文件描述了项目如何被构建，最后生成Ninja文件以执行实际构建。
29. **Bake**: 一种嵌入式开发领域的构建生成工具，用于自动生成嵌入式系统的构建脚本和配置文件。
30. **Rebar3**: 用于Erlang项目的构建和生成工具，提供了项目依赖管理、打包等功能，支持生成项目结构和相关配置。
31. **PicoSDK**: 专为树莓派Pico设计的构建生成工具，帮助开发者自动生成CMake配置文件，简化嵌入式项目的构建过程。
