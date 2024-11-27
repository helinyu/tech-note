# groovy vs Kotlin

在 Android Studio 创建新项目时，`Build Configuration Language` 选项指定了你用于配置构建脚本的语言。这决定了你项目中 **Gradle** 构建文件的语法和方式。具体来说，它有两个主要选项：

1. **Groovy**（默认选项）
2. **Kotlin**

#### 1. **Groovy**

* **Groovy** 是 Gradle 默认使用的脚本语言。使用 Groovy 语言时，Gradle 的构建脚本通常使用 `.gradle` 扩展名。Groovy 语法灵活且简单，广泛用于许多老旧的 Android 项目。
*   示例（`build.gradle`）：

    ```groovy
    plugins {
        id 'com.android.application'
    }

    android {
        compileSdkVersion 33
        defaultConfig {
            applicationId "com.example.myapp"
            minSdkVersion 21
            targetSdkVersion 33
        }
    }
    ```

#### 2. **Kotlin**

* **Kotlin** 作为 Gradle 构建脚本语言越来越流行，特别是在 Android 开发中。Kotlin 具有静态类型、类型安全等优势，提供了更好的 IDE 支持和自动补全功能，同时还能够减少错误。
* 如果选择 Kotlin，构建文件会使用 `.kts`（Kotlin Script）扩展名。
*   示例（`build.gradle.kts`）：

    ```kotlin
    plugins {
        id("com.android.application")
    }

    android {
        compileSdk = 33
        defaultConfig {
            applicationId = "com.example.myapp"
            minSdk = 21
            targetSdk = 33
        }
    }
    ```

#### 选择 **Kotlin** 或 **Groovy** 作为构建语言的影响

* **Kotlin DSL**（Kotlin Script）提供更好的类型安全、编译时错误检查和更强大的工具支持（如 IntelliJ IDEA 的代码补全和类型推导）。
* **Groovy** 提供的是更传统的语法，虽然较为灵活，但缺乏静态类型检查，容易引入运行时错误，特别是随着项目规模的增大。

#### 总结

* 如果你希望拥有更强的类型安全、代码补全支持，以及更现代化的语法，选择 **Kotlin** 作为构建配置语言。
* 如果你已经熟悉 Groovy 或者是在维护老旧的项目，选择 **Groovy** 也是一个不错的选择。
