# UI布局

* **特点**：允许更复杂的布局结构，子视图的大小和位置可以通过设置约束关系来决定。
* **用法**：适合构建响应式布局，减少嵌套层级。
*   **示例**：

    ```xml
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/textView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello, World!"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintStart_toStartOf="parent" />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Click Me"
            app:layout_constraintTop_toBottomOf="@id/textView"
            app:layout_constraintStart_toStartOf="parent" />
    </androidx.constraintlayout.widget.ConstraintLayout>
    ```

#### 4. **网格布局（GridLayout）**

* **特点**：允许将子视图放置在网格中。
* **用法**：可以通过指定行和列来定义视图的位置。
*   **示例**：

    ```xml
    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="2">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Item 1" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Item 2" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Item 3" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Item 4" />
    </GridLayout>
    ```

#### 5. **帧布局（FrameLayout）**

* **特点**：用于在同一个位置堆叠多个视图，通常用于显示单个子视图。
* **用法**：可以通过 `layout_gravity` 属性来调整子视图的对齐方式。
*   **示例**：

    ```xml
    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/image" />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Click Me"
            android:layout_gravity="center" />
    </FrameLayout>
    ```

#### 6. **滚动视图（ScrollView）**

* **特点**：用于使其子视图可以垂直滚动。
* **用法**：通常与其他布局组合使用。
*   **示例**：

    ```xml
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Long content here..." />
            <!-- 更多视图 -->
        </LinearLayout>
    </ScrollView>
    ```

#### 小结

Android 提供了多种布局方式，帮助开发者构建丰富的用户界面。选择合适的布局可以提升应用的用户体验，并确保在不同屏幕尺寸和方向下的良好显示效果。
