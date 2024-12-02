# 生命周期： Activity vs App

在 **Android 开发** 中，`Activity` 的生命周期和整个 `App` 的生命周期是两个密切相关但有所不同的概念。以下是它们的对比分析：

***

#### **1. Activity 的生命周期**

`Activity` 是 Android 中的一个核心组件，用于呈现用户界面。它的生命周期由以下几个主要状态组成，这些状态是由用户交互或系统事件触发的：

**生命周期方法：**

1. **`onCreate()`**
   * 活动被创建时调用。
   * 初始化界面、设置布局等。
2. **`onStart()`**
   * 活动变为可见，但尚未进入前台交互状态。
3. **`onResume()`**
   * 活动进入前台，可以与用户交互。
   * 此时是活动的“运行状态”。
4. **`onPause()`**
   * 活动失去焦点，但仍可见（如打开对话框或切换到另一个活动）。
   * 应保存临时数据或停止耗资源的任务。
5. **`onStop()`**
   * 活动完全不可见（如返回桌面或启动另一个活动）。
   * 可以释放资源。
6. **`onDestroy()`**
   * 活动被销毁时调用，通常用于清理资源。
7. **`onRestart()`**
   * 活动从不可见状态重新启动。

**Activity 生命周期特点：**

* 生命周期较短，受用户行为和系统事件影响明显。
* 可以存在多个 Activity 彼此切换，但它们的生命周期是独立的。
* 主要用于管理一个界面单元的行为。

***

#### **2. App 的生命周期**

`App` 的生命周期是指整个应用程序的生命周期，从启动到终止，覆盖了多个组件（Activity、Service 等）。

**主要表现形式：**

1. **启动：**
   * App 被首次启动时，`Application` 对象会被创建并调用 `onCreate()` 方法。
2. **运行：**
   * 在 App 的任何组件（如 Activity、Service）被调用期间，App 都处于运行状态。
3. **后台：**
   * 所有的 Activity 都停止时，App 进入后台，但进程未被杀死。
4. **终止：**
   * 系统资源紧张时，后台 App 可能会被杀死。此时，`Application` 的对象会被回收。

**Application 生命周期相关方法：**

1. **`onCreate()`**
   * 在 App 进程启动时调用，通常用于初始化全局资源（如依赖注入框架、日志系统等）。
2. **`onLowMemory()` / `onTrimMemory()`**
   * 系统资源不足时调用，用于提示释放内存。
3. **`onTerminate()`**
   * 在模拟环境中用于清理资源（不会在生产环境中调用）。

**App 生命周期特点：**

* 生命周期长，覆盖整个应用进程的存续时间。
* 涉及到整个应用的初始化和全局状态管理。

***

#### **对比总结**

| 特性       | **Activity 生命周期**                 | **App 生命周期**                           |
| -------- | --------------------------------- | -------------------------------------- |
| **控制范围** | 单个界面组件                            | 整个应用程序                                 |
| **开始时机** | 每次启动一个 Activity 时触发               | 应用启动时（Application 被创建时）                |
| **结束时机** | Activity 被销毁时触发                   | 应用进程终止时                                |
| **粒度**   | 细粒度，关注具体界面的操作                     | 粗粒度，关注应用级别的状态                          |
| **关联方法** | `onCreate`、`onStart`、`onResume` 等 | `Application.onCreate`、`onLowMemory` 等 |
| **影响因素** | 用户操作、Activity 跳转、系统回收等            | 系统内存管理、应用前后台切换、用户主动退出等                 |
| **用途**   | 管理单个界面组件的状态和行为                    | 管理全局资源和应用级别的状态                         |

***

#### **联系**

* 每个 `Activity` 的生命周期方法是应用生命周期中的子部分。
* `Application` 是管理全局状态的入口，而 `Activity` 专注于具体界面的用户体验。