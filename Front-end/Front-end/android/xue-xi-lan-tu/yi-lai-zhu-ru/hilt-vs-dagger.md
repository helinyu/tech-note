# Hilt vs Dagger

在 Android 开发中，**Dagger** 和 **Hilt** 是两种用于依赖注入（Dependency Injection, DI）的框架。**Hilt** 是 **Dagger** 的一个简化版，专为 Android 应用而设计，旨在降低学习成本并提升开发效率。以下是它们的对比分析：

***

#### **1. Dagger**

**特点：**

* **Dagger 2** 是一个全功能的 DI 框架，由 Google 开发。
* 编译时生成依赖关系，性能优秀。
* 高度灵活，支持复杂的 DI 场景。
* 与平台无关，可用于 Android、Java 项目。

**优点：**

1. **灵活性高**：可以自由定制依赖的范围（Scope）和生命周期。
2. **性能优越**：编译时生成代码，运行时效率高。
3. **成熟性**：适用于各种复杂的依赖注入需求。

**缺点：**

1. **学习曲线陡峭**：需要理解较多概念，如 `@Component`、`@Module`、`@Scope`。
2. **配置复杂**：需要手动定义 Component 和 Module，代码量较多。
3. **整合成本高**：与 Android 的集成需要更多手动工作。

**适用场景：**

* 非 Android 项目或复杂的 Android 应用中，需要灵活定义依赖的生命周期和作用域。
* 项目对性能有极高要求。

***

#### **2. Hilt**

**特点：**

* 基于 Dagger，专为 Android 设计的 DI 框架。
* 内置了与 Android 生命周期组件的紧密集成（如 `Activity`、`Fragment`）。
* 使用注解自动生成必要的 Component 和 Module，大幅减少手动工作。

**优点：**

1. **简化开发**：提供预定义的 `Component`（如 `@ApplicationComponent`），开发者只需关注核心逻辑。
2. **易于学习**：封装了复杂的 Dagger 配置，使用方式更直观。
3. **与 Android 生命周期集成**：依赖的 Scope 与 Android 组件（如 `ViewModel`、`Activity`）的生命周期一致。
4. **官方推荐**：Google 明确推荐 Hilt 作为 Android 开发的 DI 框架。

**缺点：**

1. **灵活性略低**：预定义的 Component 适用于大多数场景，但对特殊需求支持不足。
2. **仅限 Android**：设计上依赖 Android 框架，不能直接用于非 Android 项目。
3. **部分复杂场景需要手动回退到 Dagger**。

**适用场景：**

* Android 应用开发，特别是需要快速实现 DI 的项目。
* 中小型应用或对 DI 灵活性需求不高的项目。

***

#### **对比总结**

| 特性               | **Dagger**                | **Hilt**                         |
| ---------------- | ------------------------- | -------------------------------- |
| **学习成本**         | 较高，需要熟悉 DI 概念和 Dagger 配置  | 较低，简化了 Dagger 的复杂配置              |
| **灵活性**          | 非常高，支持复杂 DI 场景            | 较低，依赖 Android 组件，支持的范围有限         |
| **自动化程度**        | 需要手动配置 Component 和 Module | 高度自动化，通过注解生成 Component           |
| **性能**           | 高，编译时生成依赖代码，运行效率高         | 高，底层仍然使用 Dagger                  |
| **与 Android 集成** | 手动配置，较复杂                  | 内置集成，如 `@ActivityRetainedScoped` |
| **适用场景**         | 复杂项目、需要完全掌控 DI 的生命周期      | Android 项目，快速实现依赖注入              |

***

#### **适配 Android 生命周期**

Hilt 提供了与 Android 生命周期组件紧密结合的作用域（Scope），这是其相较于 Dagger 的最大优势之一：

| **Scope**                 | **作用范围**                                   |
| ------------------------- | ------------------------------------------ |
| `@Singleton`              | 应用级别，依赖在整个应用生命周期中共享                        |
| `@ActivityRetainedScoped` | 在 `ViewModel` 生命周期中共享，适合跨 `Activity` 使用的依赖 |
| `@ActivityScoped`         | `Activity` 级别的依赖，绑定到 Activity 生命周期         |
| `@FragmentScoped`         | `Fragment` 级别的依赖，绑定到 Fragment 生命周期         |
| `@ViewScoped`             | `View` 级别的依赖，绑定到 `View`（如 `Custom View`）   |
| `@ViewModelScoped`        | 绑定到 `ViewModel` 的生命周期                      |

***

#### **选择建议**

1. **使用 Hilt：**
   * **快速开发：** 小型到中型 Android 项目。
   * **新手：** 对依赖注入不熟悉，优先选择 Hilt。
   * **Google 推荐：** 官方支持强，未来维护成本较低。
2. **使用 Dagger：**
   * **非 Android 项目：** 需要跨平台或不依赖 Android 的 DI 解决方案。
   * **高级场景：** DI 需求复杂，Hilt 的预定义 Scope 无法满足需求。
   * **性能要求：** 极高性能的复杂依赖场景。

对于大多数现代 Android 项目，**Hilt 是首选**。但对于需要更高灵活性或非标准 DI 场景的项目，可以回退到 **Dagger**。
