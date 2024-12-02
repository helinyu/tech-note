# 配置底部的Tabbar

在 Android 项目中，配置底部的 TabBar（通常使用 `BottomNavigationView` 实现）是一个常见的 UI 组件。`BottomNavigationView` 提供了一个方便的方式来展示多个 `Fragment`，并允许用户在不同的屏幕之间进行切换。接下来，我们将详细说明如何在 Android 中配置底部的 TabBar，并结合 `Navigation` 组件实现多 `Fragment` 导航。

#### 1. **添加依赖**

首先，确保你的 `build.gradle` 文件中已包含所需的依赖。

```groovy
dependencies {
    implementation "com.google.android.material:material:1.7.0" // 确保已添加Material Components库
    implementation "androidx.navigation:navigation-fragment-ktx:2.5.0" // 导航组件依赖
    implementation "androidx.navigation:navigation-ui-ktx:2.5.0" // UI组件依赖
}
```

* `material`：Material Design 库，包含 `BottomNavigationView`。
* `navigation-fragment` 和 `navigation-ui`：用于实现 `Fragment` 导航和与 UI 控件（如 `BottomNavigationView`）集成。

#### 2. **创建布局文件**

在你的布局 XML 文件中，添加 `BottomNavigationView`，并通过 `FragmentContainerView` 或 `NavHostFragment` 来容纳 `Fragment`。

```xml
<!-- activity_main.xml -->
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- 主内容区，用来承载 Fragment -->
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:defaultNavHost="true"  <!-- 使得返回键返回到 Navigation 栈 -->
        app:navGraph="@navigation/nav_graph" /> <!-- 导航图 -->

    <!-- 底部导航栏 -->
    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottom_nav"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        app:menu="@menu/bottom_nav_menu" <!-- 引用菜单资源 -->
        app:itemIconTint="@color/nav_item_color"   <!-- 设置选中和未选中的颜色 -->
        app:itemTextColor="@color/nav_item_color" />
</androidx.coordinatorlayout.widget.CoordinatorLayout>
```

* **`FragmentContainerView`**: 用来容纳和显示导航图中定义的 `Fragment`。你可以选择使用 `FragmentContainerView` 或 `NavHostFragment`（`NavHostFragment` 是 `Fragment` 容器的传统实现）。
* **`BottomNavigationView`**: 放置底部的导航栏，它使用菜单资源来定义底部 Tab 的选项。

#### 3. **创建底部导航菜单**

接下来，创建一个菜单文件，通常位于 `res/menu/` 目录下。每个菜单项对应一个 `Fragment`。

例如，在 `res/menu/` 目录下创建 `bottom_nav_menu.xml` 文件：

```xml
<!-- bottom_nav_menu.xml -->
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/home"
        android:icon="@drawable/ic_home"
        android:title="Home" />
    <item
        android:id="@+id/search"
        android:icon="@drawable/ic_search"
        android:title="Search" />
    <item
        android:id="@+id/settings"
        android:icon="@drawable/ic_settings"
        android:title="Settings" />
</menu>
```

* 每个 `item` 标签表示底部 Tab 上的一个选项。
* `android:id` 用于唯一标识每个菜单项。
* `android:icon` 和 `android:title` 分别设置每个 Tab 的图标和标题。

#### 4. **配置 Navigation 图（NavGraph）**

在 `res/navigation/` 目录下创建一个 `nav_graph.xml` 文件，定义与底部导航栏关联的各个 `Fragment`。

```xml
<!-- nav_graph.xml -->
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/nav_graph"
    app:startDestination="@id/fragment_home">

    <fragment
        android:id="@+id/fragment_home"
        android:name="com.example.app.ui.HomeFragment"
        android:label="Home"
        app:destination="@id/fragment_search" />

    <fragment
        android:id="@+id/fragment_search"
        android:name="com.example.app.ui.SearchFragment"
        android:label="Search" />

    <fragment
        android:id="@+id/fragment_settings"
        android:name="com.example.app.ui.SettingsFragment"
        android:label="Settings" />
</navigation>
```

* **`startDestination`**：定义应用启动时显示的默认 Fragment。
* **`fragment`**：每个 `Fragment` 对应底部菜单中的一个选项。

#### 5. **在 `Activity` 中设置 `BottomNavigationView`**

在 `Activity` 中，使用 `NavController` 和 `BottomNavigationView` 来实现底部 Tab 的切换和导航操作。

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 获取 NavController
        val navController = findNavController(R.id.nav_host_fragment)

        // 获取 BottomNavigationView
        val bottomNav: BottomNavigationView = findViewById(R.id.bottom_nav)

        // 将 BottomNavigationView 与 NavController 绑定
        NavigationUI.setupWithNavController(bottomNav, navController)
    }
}
```

* `findNavController(R.id.nav_host_fragment)`：获取 `NavController`，它负责管理 `Fragment` 之间的导航。
* `NavigationUI.setupWithNavController(bottomNav, navController)`：将 `BottomNavigationView` 和 `NavController` 绑定起来，让底部导航与 `NavController` 协同工作，实现 Tab 切换。

#### 6. **管理底部导航栏的状态**

如果你希望在切换 `Fragment` 时，底部导航栏能够正确反映当前选中的 Tab 状态，`NavigationUI.setupWithNavController()` 会自动管理这个状态。但是如果你需要进行自定义处理，可以通过以下代码手动设置选中状态：

```kotlin
bottomNav.selectedItemId = R.id.home // 默认选中首页
```

#### 7. **处理返回键**

默认情况下，`BottomNavigationView` 会自动处理 `Fragment` 间的返回操作。但如果需要自定义返回行为，可以重写 `onBackPressed` 方法：

```kotlin
override fun onBackPressed() {
    val navController = findNavController(R.id.nav_host_fragment)
    if (!navController.navigateUp()) {
        super.onBackPressed()
    }
}
```

#### 8. **使用 SafeArgs 传递数据（可选）**

如果你需要在不同的 `Fragment` 之间传递数据，可以使用 **SafeArgs**，这是 `Navigation` 提供的安全的类型化参数传递方式。

1.  在 `build.gradle` 文件中启用 `SafeArgs` 插件：

    ```groovy
    plugins {
        id 'androidx.navigation.safeargs.kotlin'
    }
    ```
2. 定义参数并在导航时传递数据：

```xml
<fragment
    android:id="@+id/fragment_search"
    android:name="com.example.app.ui.SearchFragment"
    android:label="Search">
    <argument
        android:name="query"
        app:argType="string" />
</fragment>
```

3. 通过 `SafeArgs` 在导航时传递参数：

```kotlin
val action = HomeFragmentDirections.actionHomeFragmentToSearchFragment("query text")
findNavController().navigate(action)
```

4. 在目标 `Fragment` 中获取参数：

```kotlin
val args: SearchFragmentArgs by navArgs()
val query = args.query
```

#### 总结

配置底部 TabBar 涉及以下关键步骤：

1. 使用 `BottomNavigationView` 创建底部导航栏，并定义菜单项。
2. 使用 `NavController` 和 `NavHostFragment` 来管理 `Fragment` 之间的导航。
3. 将 `BottomNavigationView` 和 `NavController` 结合，自动切换 Tab 和管理导航状态。
4. 使用 `SafeArgs` 传递安全的参数（可选）。

通过这种方式，你可以实现一个功能齐全、易于维护的底部 TabBar，同时结合 `Navigation` 组件来简化 Fragment 间的导航逻辑。
