# Activity vs Fragment

* **Activity 是容器**：Activity 是一个单独的用户界面组件，负责管理用户交互和应用的 UI。Fragment 通常嵌入到 Activity 中，作为 Activity 用户界面的一部分。
* **Fragment 是子组件**：Fragment 是可以在 Activity 中重用和组合的 UI 组件，提供了更细粒度的 UI 管理。

#### 2. **生命周期管理**

* **生命周期关联**：Fragment 的生命周期依赖于其所附加的 Activity。当 Activity 处于不同状态（如创建、启动、暂停等）时，Fragment 的生命周期方法也会被调用。
* **独立性**：虽然 Fragment 的生命周期受 Activity 控制，但它有自己独立的生命周期回调方法，比如 `onCreateView()` 和 `onDestroyView()`，用于管理视图的创建和销毁。

#### 3. **交互**

* **数据共享**：Fragment 可以通过与其宿主 Activity 交互来共享数据。通常，这通过定义接口来实现，Activity 实现这些接口以接收来自 Fragment 的回调。
* **回调方法**：Fragment 可以调用其宿主 Activity 中的方法，Activity 也可以通过 FragmentManager 与 Fragment 进行通信。

#### 4. **重用性**

* **可重用性**：Fragment 是模块化的，可以在多个 Activity 中重用，而 Activity 通常代表一个应用的独立界面。
* **动态添加**：可以在运行时动态添加、替换或移除 Fragment，使得 UI 结构更加灵活。

#### 5. **导航**

* **Fragment 导航**：在使用 Fragment 时，可以在一个 Activity 中通过不同的 Fragment 实现应用内导航，而不必启动新的 Activity。这样可以实现更流畅的用户体验。

#### 示例代码

以下是一个简单示例，展示如何在 Activity 中使用 Fragment：

**Activity 示例：**

```java
public class MainActivity extends AppCompatActivity {
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 动态添加 Fragment
        if (savedInstanceState == null) {
            MyFragment myFragment = new MyFragment();
            getSupportFragmentManager().beginTransaction()
                .add(R.id.fragment_container, myFragment)
                .commit();
        }
    }
}
```

**Fragment 示例：**

```java
public class MyFragment extends Fragment {
    
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_my, container, false);
    }

    // 其他 Fragment 方法
}
```

#### 小结

Activity 和 Fragment 的关系是构建 Android 应用的重要组成部分。Activity 作为宿主，负责管理 Fragment 的生命周期和交互，而 Fragment 提供了更灵活、可重用的 UI 组件。
