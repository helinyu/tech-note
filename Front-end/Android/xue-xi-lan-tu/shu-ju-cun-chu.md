# 数据存储

SQlite 就不说了。

在 Android 开发中，持久化数据是一个重要的主题，常用的方法包括 Room 持久化库和 SharedPreferences。以下是这两者的详细介绍：

#### 1. **Room 持久化库**

Room 是 Android Jetpack 组件中的一部分，提供了一个抽象层，以便在 SQLite 数据库上更容易地进行操作。它帮助开发者以对象的形式访问数据库，简化了数据库的管理和查询。

**主要特点**

* **对象映射**：Room 允许将数据库表映射到 Java/Kotlin 对象，从而避免手动编写 SQL 代码。
* **编译时检查**：通过注解处理器，Room 可以在编译时检查 SQL 查询的正确性，减少运行时错误。
* **支持 LiveData 和 RxJava**：Room 可以与 LiveData 和 RxJava 一起使用，实现响应式编程。
* **事务支持**：Room 支持事务，确保数据操作的原子性。

**使用示例**

1.  **添加依赖**：

    ```gradle
    implementation "androidx.room:room-runtime:2.5.0"
    annotationProcessor "androidx.room:room-compiler:2.5.0" // For Java
    kapt "androidx.room:room-compiler:2.5.0" // For Kotlin
    ```
2.  **定义实体类**：

    ```java
    @Entity(tableName = "user")
    public class User {
        @PrimaryKey
        @NonNull
        private String uid;

        private String name;
        
        // Getters and Setters
    }
    ```
3.  **定义 DAO（数据访问对象）**：

    ```java
    @Dao
    public interface UserDao {
        @Insert
        void insert(User user);

        @Query("SELECT * FROM user WHERE uid = :uid")
        User getUserById(String uid);
    }
    ```
4.  **定义数据库**：

    ```java
    @Database(entities = {User.class}, version = 1)
    public abstract class AppDatabase extends RoomDatabase {
        public abstract UserDao userDao();
    }
    ```
5.  **使用 Room 数据库**：

    ```java
    AppDatabase db = Room.databaseBuilder(getApplicationContext(),
            AppDatabase.class, "database-name").build();
    ```

#### 2. **SharedPreferences**

SharedPreferences 是 Android 提供的一种轻量级的数据存储方式，主要用于存储简单的键值对（key-value pairs）。它适用于存储小量的用户设置或应用配置。

**主要特点**

* **轻量级**：适合存储简单的应用配置或用户偏好设置。
* **简单易用**：使用简单的 API 操作。
* **异步存储**：可以通过异步方法进行存储，以防止阻塞主线程。

**使用示例**

1.  **获取 SharedPreferences 实例**：

    ```java
    SharedPreferences sharedPreferences = getSharedPreferences("my_prefs", MODE_PRIVATE);
    ```
2.  **存储数据**：

    ```java
    SharedPreferences.Editor editor = sharedPreferences.edit();
    editor.putString("username", "JohnDoe");
    editor.putInt("user_age", 30);
    editor.apply(); // 或使用 editor.commit() 进行同步存储
    ```
3.  **读取数据**：

    ```java
    String username = sharedPreferences.getString("username", "defaultUser");
    int userAge = sharedPreferences.getInt("user_age", 0);
    ```
4.  **删除数据**：

    ```java
    SharedPreferences.Editor editor = sharedPreferences.edit();
    editor.remove("username");
    editor.apply();
    ```

#### 小结

* **Room 持久化库**：适合存储结构化数据（如复杂对象和关系），提供强大的数据库功能和对象映射。
* **SharedPreferences**：适合存储简单的配置和用户设置，使用简单且轻量级。

选择合适的持久化方式可以帮助开发者更高效地管理应用的数据。对于复杂的数据，推荐使用 Room；而对于简单的设置或偏好，则可以使用 SharedPreferences。
