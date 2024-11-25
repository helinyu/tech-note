# 依赖注入

依赖注入（Dependency Injection，DI）是一种软件设计模式，用于实现控制反转（Inversion of Control，IoC）。在这个模式中，对象不需要自己创建依赖项，而是通过构造函数、属性或接口来接受其依赖项。依赖注入有助于提高代码的可测试性、可维护性和可重用性。

在 Android 开发中，使用依赖注入框架可以简化依赖项的管理，常用的依赖注入框架包括 Dagger 和 Hilt。

#### 1. **Dagger**

Dagger 是一个静态依赖注入框架，由 Google 开发。它生成代码以处理依赖项注入，从而在运行时提高性能。

**基本概念**

* **@Module**：提供依赖项的方法集合。
* **@Provides**：标记一个方法，以便它可以提供某种依赖项。
* **@Inject**：标记构造函数、字段或方法，以便 Dagger 知道如何提供依赖项。
* **@Component**：将模块和依赖项连接在一起的接口。

**使用示例**

1.  **添加依赖**： 在 `build.gradle` 中添加：

    ```gradle
    implementation 'com.google.dagger:dagger:2.45'
    annotationProcessor 'com.google.dagger:dagger-compiler:2.45' // For Java
    kapt 'com.google.dagger:dagger-compiler:2.45' // For Kotlin
    ```
2.  **定义模块**：

    ```java
    @Module
    public class NetworkModule {
        @Provides
        public OkHttpClient provideOkHttpClient() {
            return new OkHttpClient();
        }

        @Provides
        public Retrofit provideRetrofit(OkHttpClient client) {
            return new Retrofit.Builder()
                    .client(client)
                    .baseUrl("https://api.example.com/")
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }
    }
    ```
3.  **定义组件**：

    ```java
    @Component(modules = {NetworkModule.class})
    public interface AppComponent {
        void inject(MainActivity activity);
    }
    ```
4.  **使用依赖项**：

    ```java
    public class MainActivity extends AppCompatActivity {
        @Inject
        Retrofit retrofit;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            // 初始化 Dagger
            AppComponent component = DaggerAppComponent.create();
            component.inject(this);
        }
    }
    ```

#### 2. **Hilt**

Hilt 是基于 Dagger 的一个依赖注入库，简化了 Dagger 的使用，使得在 Android 应用中使用依赖注入变得更加容易。

**基本概念**

* **@HiltAndroidApp**：标记应用程序类，以启用 Hilt。
* **@AndroidEntryPoint**：标记 Android 组件（如 Activity、Fragment、Service）以使用 Hilt 注入。
* **@Inject**：标记依赖项，以便 Hilt 可以提供它们。
* **@Module** 和 **@InstallIn**：定义模块并指定其生命周期。

**使用示例**

1.  **添加依赖**： 在 `build.gradle` 中添加：

    ```gradle
    implementation 'com.google.dagger:hilt-android:2.45'
    kapt 'com.google.dagger:hilt-compiler:2.45'
    ```
2.  **应用程序类**：

    ```java
    @HiltAndroidApp
    public class MyApplication extends Application {
    }
    ```
3.  **定义模块**：

    ```java
    @Module
    @InstallIn(SingletonComponent.class)
    public class NetworkModule {
        @Provides
        @Singleton
        public OkHttpClient provideOkHttpClient() {
            return new OkHttpClient();
        }

        @Provides
        @Singleton
        public Retrofit provideRetrofit(OkHttpClient client) {
            return new Retrofit.Builder()
                    .client(client)
                    .baseUrl("https://api.example.com/")
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }
    }
    ```
4.  **使用依赖项**：

    ```java
    @AndroidEntryPoint
    public class MainActivity extends AppCompatActivity {
        @Inject
        Retrofit retrofit;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            // 使用 retrofit 进行网络请求
        }
    }
    ```

#### 小结

依赖注入（DI）是一种有效的设计模式，能够提高代码的可维护性和可测试性。在 Android 开发中，Dagger 和 Hilt 是两种流行的依赖注入框架，能够简化依赖项的管理。选择适合的依赖注入框架，可以帮助开发者更高效地构建和维护应用程序。
