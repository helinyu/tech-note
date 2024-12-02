# 配置navigation

在 Android 项目中，`Navigation` 是一个帮助你实现应用内屏幕导航的组件，它使得在不同的屏幕间切换变得更加简洁和高效。`Navigation` 的配置包括以下几个步骤：

#### 1. **添加 Navigation 依赖**

在你的 `app/build.gradle` 文件中，添加 `Navigation` 组件的依赖。通常会使用如下依赖：

```groovy
dependencies {
    def nav_version = "2.5.0"  // 适当更改版本号

    implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
    implementation "androidx.navigation:navigation-ui-ktx:$nav_version"
}
```

* `navigation-fragment-ktx`: 允许你在 `Fragment` 中使用 `Navigation`。
* `navigation-ui-ktx`: 提供与 UI 组件（如 `Toolbar`、`BottomNavigationView`）的集成。

#### 2. **创建 Navigation 图（NavGraph）**

`Navigation` 使用 **导航图（NavGraph）** 来定义应用中所有的屏幕和它们之间的导航关系。你可以通过以下两种方式创建导航图：

**1.1 通过 XML 文件创建**

最常见的方式是通过 XML 文件创建导航图。这个文件通常位于 `res/navigation/` 目录中。你可以在 Android Studio 中右键点击 `res` 文件夹，选择 **New → Android Resource File**，然后选择类型为 `Navigation`，文件名可以是 `nav_graph.xml` 或其他。

示例 `nav_graph.xml`：

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/nav_graph"
    app:startDestination="@id/fragment_home">

    <fragment
        android:id="@+id/fragment_home"
        android:name="com.example.app.ui.HomeFragment"
        android:label="Home"
        app:destination="@id/fragment_details" />

    <fragment
        android:id="@+id/fragment_details"
        android:name="com.example.app.ui.DetailsFragment"
        android:label="Details" />
</navigation>
```

* `startDestination`: 定义应用启动时的第一个屏幕。
* `fragment`: 定义各个 `Fragment` 和它们之间的导航关系。
* `android:name`: 该属性指定了每个屏幕对应的 `Fragment` 类。

**1.2 通过代码创建**

如果你更倾向于编程方式构建导航图，可以使用 `NavController` 和 `NavGraph` 类进行配置。

```kotlin
val navController = findNavController(R.id.nav_host_fragment)
val navInflater = navController.navInflater
val navGraph = navInflater.inflate(R.navigation.nav_graph)
navController.graph = navGraph
```

#### 3. **设置 NavHostFragment**

为了使用 `Navigation`，你需要在你的布局文件中添加一个 `NavHostFragment`，它是应用导航的容器，所有的 `Fragment` 都将被添加到这个容器中。

示例：

```xml
<androidx.fragment.app.FragmentContainerView
    android:id="@+id/nav_host_fragment"
    android:name="androidx.navigation.fragment.NavHostFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:navGraph="@navigation/nav_graph"
    app:defaultNavHost="true" />
```

* `app:navGraph`: 指定应用的导航图文件。
* `app:defaultNavHost`: 将此 `NavHostFragment` 设置为默认导航主机。

#### 4. **通过 NavController 进行导航操作**

在 `Fragment` 或 `Activity` 中，你可以使用 `NavController` 进行屏幕间的导航。通常，`NavController` 会与 UI 控件（如按钮、菜单项）结合使用。

**4.1 导航到指定的 Fragment**

```kotlin
// 获取 NavController
val navController = findNavController()

// 导航到目标 Fragment
navController.navigate(R.id.action_homeFragment_to_detailsFragment)
```

**4.2 传递参数（安全的方式）**

你可以在导航时传递参数，通过 `SafeArgs` 插件生成类型安全的导航代码。

* 先在 `build.gradle` 文件中启用 `SafeArgs` 插件：

```groovy
apply plugin: "androidx.navigation.safeargs.kotlin"
```

* 然后在导航图中定义参数：

```xml
<fragment
    android:id="@+id/fragment_details"
    android:name="com.example.app.ui.DetailsFragment"
    android:label="Details">
    <argument
        android:name="itemId"
        app:argType="string" />
</fragment>
```

* 在导航时传递参数：

```kotlin
val action = HomeFragmentDirections.actionHomeFragmentToDetailsFragment("123")
findNavController().navigate(action)
```

* 在目标 `Fragment` 中获取参数：

```kotlin
val args: DetailsFragmentArgs by navArgs()
val itemId = args.itemId
```

#### 5. **与 UI 组件的集成**

`Navigation` 还可以与 UI 组件（如 `Toolbar`、`BottomNavigationView`）集成。

**5.1 与 Toolbar 集成**

你可以通过 `NavigationUI` 将 `Toolbar` 与导航图结合，让 `Toolbar` 响应后退事件。

```kotlin
val navController = findNavController(R.id.nav_host_fragment)
NavigationUI.setupActionBarWithNavController(this, navController)
```

* 在 `Activity` 中重写 `onSupportNavigateUp` 方法，处理返回操作：

```kotlin
override fun onSupportNavigateUp(): Boolean {
    return findNavController(R.id.nav_host_fragment).navigateUp() || super.onSupportNavigateUp()
}
```

**5.2 与 BottomNavigationView 集成**

你可以将 `BottomNavigationView` 与 `Navigation` 结合，使用 `NavigationUI.setupWithNavController()` 实现点击底部导航按钮时的导航。

```kotlin
val navController = findNavController(R.id.nav_host_fragment)
val bottomNav: BottomNavigationView = findViewById(R.id.bottom_nav)
NavigationUI.setupWithNavController(bottomNav, navController)
```

#### 6. **处理返回栈（Back Stack）**

`Navigation` 组件会自动处理返回栈（`Back Stack`）。例如，当你从一个 `Fragment` 导航到另一个 `Fragment` 时，系统会自动保存当前的屏幕状态，按返回键时自动返回到上一个屏幕。如果需要自定义返回行为，可以使用 `NavController` 的方法控制：

```kotlin
findNavController().popBackStack() // 返回到上一个屏幕
```

#### 7. **处理深度链接（Deep Links）**

`Navigation` 还支持深度链接，可以通过配置 `NavGraph` 实现从外部链接直接跳转到应用中的特定页面。

在导航图中定义深度链接：

```xml
<fragment
    android:id="@+id/fragment_details"
    android:name="com.example.app.ui.DetailsFragment"
    android:label="Details">
    <deepLink
        android:id="@+id/deep_link"
        app:uri="https://www.example.com/details/{itemId}" />
</fragment>
```

在你的应用中，处理深度链接：

```kotlin
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.example.com/details/123"))
startActivity(intent)
```

#### 总结

配置 Android Navigation 组件的过程包括以下几个步骤：

1. **添加依赖**：将 Navigation 相关库添加到 `build.gradle` 文件中。
2. **创建 NavGraph**：使用 XML 文件或代码创建导航图，定义各个 `Fragment` 和它们之间的导航关系。
3. **设置 NavHostFragment**：在布局文件中添加 `NavHostFragment`，用来显示导航图中的 `Fragment`。
4. **执行导航操作**：使用 `NavController` 执行导航操作，可以传递参数并且管理返回栈。
5. **集成 UI 组件**：与 `Toolbar`、`BottomNavigationView` 等 UI 控件集成，简化导航操作。

`Navigation` 组件的主要优点是减少了重复的代码，简化了屏幕间的导航逻辑，支持类型安全的参数传递和深度链接等功能，是现代 Android 开发中非常推荐的导航解决方案。
