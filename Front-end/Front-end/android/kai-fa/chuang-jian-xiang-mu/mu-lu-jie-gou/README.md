# 目录结构

在一个典型的安卓项目中，目录结构通常如下所示：

```
MyApplication/
├── app/                           # 应用模块
│   ├── build.gradle               # 应用模块的构建脚本
│   ├── src/                       # 应用源代码
│   │   ├── main/                  
│   │   │   ├── java/              # Java 源代码
│   │   │   │   └── com/           # 包名（根据你项目的实际包名）
│   │   │   ├── res/               # 资源文件
│   │   │   │   ├── drawable/      # 图片等图形资源
│   │   │   │   ├── layout/        # 布局文件（.xml）
│   │   │   │   ├── mipmap/        # 各种图标资源
│   │   │   │   ├── values/        # 字符串、颜色、样式等资源
│   │   │   │   └── raw/           # 原始文件，如音频、视频、txt文件等
│   │   │   ├── AndroidManifest.xml# 应用的清单文件
│   │   │   └── assets/            # 存放原始文件（例如 HTML、字体文件等）
│   │   ├── androidTest/           # Android 测试代码
│   │   └── test/                  # 单元测试代码
├── build.gradle                   # 根项目的构建脚本
├── settings.gradle                # 配置项目构建信息的文件
└── gradle/                        # Gradle 配置目录
    └── wrapper/                   # Gradle 包装器（可选）
```

#### 主要文件和目录解释：

1. **app/src/main/java/**: 存放 Java 或 Kotlin 代码的目录，按照包名来组织（如 `com.example.app`）。
2. **app/src/main/res/**: 存放资源文件的目录，包括布局、图片、字符串、颜色、样式等。
3. **app/src/main/AndroidManifest.xml**: 定义应用的基本信息，如应用组件（活动、服务等）以及权限等。
4. **app/build.gradle**: 应用模块的 Gradle 构建脚本，定义了模块级的构建配置、依赖等。
5. **build.gradle**: 根目录下的 Gradle 构建脚本，通常用于定义全局配置、依赖库、插件等。
6. **settings.gradle**: 定义了哪些模块将会被包括到这个项目中。
7. **gradle/wrapper/**: 包含 Gradle 包装器的配置文件，这让你不需要在每个开发环境中手动安装 Gradle，可以通过项目直接使用。

