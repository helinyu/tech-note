# 数据绑定

在 Android 开发中，MVVM（Model-View-ViewModel）架构是一种常见的设计模式，旨在提高应用程序的可维护性和可测试性。为了实现 View 和 ViewModel 之间的双向数据绑定，Android 提供了几个库，最常用的有 **Android Data Binding** 和 **Jetpack Compose**。

#### 1. **Android Data Binding**

Android Data Binding 库允许开发者在布局文件中直接绑定 UI 组件到应用程序的数据源。它通过减少样板代码，使得 MVVM 架构的实现更加简单。

**基本概念**

* **Data Binding**：通过 XML 文件来绑定 UI 和数据模型。
* **LiveData**：用于观察数据变化，自动更新 UI。

**使用示例**

1.  **添加依赖**： 在 `build.gradle` 中添加：

    ```gradle
    implementation 'androidx.databinding:databinding-runtime:7.0.0'
    ```
2.  **启用 Data Binding**： 在 `build.gradle` 的 `android` 块中启用 Data Binding：

    ```gradle
    android {
        ...
        buildFeatures {
            dataBinding true
        }
    }
    ```
3.  **创建 ViewModel**：

    ```java
    public class MyViewModel extends ViewModel {
        private final MutableLiveData<String> message = new MutableLiveData<>();

        public LiveData<String> getMessage() {
            return message;
        }

        public void setMessage(String msg) {
            message.setValue(msg);
        }
    }
    ```
4.  **创建布局文件**（`activity_main.xml`）：

    ```xml
    <layout xmlns:android="http://schemas.android.com/apk/res/android">
        <data>
            <variable
                name="viewModel"
                type="com.example.MyViewModel" />
        </data>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@{viewModel.message}" />

            <Button
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:onClick="@{() -> viewModel.setMessage('Hello World!')}"
                android:text="Update Message" />
        </LinearLayout>
    </layout>
    ```
5.  **在 Activity 中设置 ViewModel**：

    ```java
    public class MainActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
            MyViewModel viewModel = new ViewModelProvider(this).get(MyViewModel.class);
            binding.setViewModel(viewModel);
            binding.setLifecycleOwner(this);
        }
    }
    ```

#### 2. **Jetpack Compose**

Jetpack Compose 是 Android 的现代 UI 工具包，提供了一种声明式的方法来构建 UI。Compose 内置了与 ViewModel 和 LiveData 的支持，使得 MVVM 架构的实现更加流畅。

**使用示例**

1.  **添加依赖**： 在 `build.gradle` 中添加：

    ```gradle
    implementation 'androidx.compose.ui:ui:1.0.0'
    implementation 'androidx.lifecycle:lifecycle-viewmodel-compose:2.0.0'
    ```
2.  **创建 ViewModel**：

    ```kotlin
    class MyViewModel : ViewModel() {
        private val _message = MutableLiveData("Initial Message")
        val message: LiveData<String> get() = _message

        fun updateMessage(newMessage: String) {
            _message.value = newMessage
        }
    }
    ```
3.  **创建 Compose UI**：

    ```kotlin
    @Composable
    fun MyScreen(viewModel: MyViewModel) {
        val message by viewModel.message.observeAsState("")

        Column {
            Text(text = message)
            Button(onClick = { viewModel.updateMessage("Hello Compose!") }) {
                Text("Update Message")
            }
        }
    }
    ```
4.  **在 Activity 中设置 Compose**：

    ```kotlin
    class MainActivity : ComponentActivity() {
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            val viewModel = ViewModelProvider(this).get(MyViewModel::class.java)

            setContent {
                MyScreen(viewModel)
            }
        }
    }
    ```

#### 小结

* **Android Data Binding**：通过 XML 文件直接绑定 UI 和 ViewModel，提高了开发效率，适合传统的 View 系统。
* **Jetpack Compose**：现代声明式 UI 工具包，提供了更简洁的语法和强大的功能，适合构建新项目。

选择适合的绑定方式取决于项目的需求和使用的 UI 技术栈。对于新的项目，推荐使用 Jetpack Compose；对于现有项目，使用 Data Binding 也是一个不错的选择。
