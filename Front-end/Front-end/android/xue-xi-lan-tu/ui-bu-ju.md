# UI布局

在安卓开发中，UI布局是通过不同的布局管理器（Layout）来控制界面元素的位置和排列。常用的布局类型有以下几种：

#### 1. **LinearLayout**

* **功能**：将子视图按照水平方向（`horizontal`）或垂直方向（`vertical`）排列。
* **常用属性**：
  * `android:orientation`：指定排列方向，`horizontal` 或 `vertical`。
  * `android:layout_width` 和 `android:layout_height`：定义布局的宽高。
  * `android:weight`：设置子视图占据的比例，结合 `android:layout_width` 或 `android:layout_height` 使用。

**示例**：

```xml
<LinearLayout
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!" />
    
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />
</LinearLayout>
```

#### 2. **RelativeLayout**

* **功能**：根据父布局或其他子视图的相对位置来放置子视图，允许更多的灵活布局。
* **常用属性**：
  * `android:layout_alignParentTop`、`android:layout_alignParentLeft` 等：指定视图与父视图的对齐方式。
  * `android:layout_toRightOf`、`android:layout_below` 等：指定视图相对于其他子视图的位置。

**示例**：

```xml
<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!"
        android:layout_centerInParent="true"/>
    
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me"
        android:layout_below="@id/textView"/>
</RelativeLayout>
```

#### 3. **ConstraintLayout**

* **功能**：一种更灵活和强大的布局方式，可以通过创建不同的约束（Constraint）来控制视图之间的关系。
* **常用属性**：
  * `app:layout_constraintLeft_toLeftOf`、`app:layout_constraintTop_toTopOf`：设置视图的约束。
  * `app:layout_constraintWidth_percent` 和 `app:layout_constraintHeight_percent`：按比例调整视图大小。

**示例**：

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"/>
    
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me"
        app:layout_constraintTop_toBottomOf="@id/textView"
        app:layout_constraintLeft_toLeftOf="parent"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

#### 4. **FrameLayout**

* **功能**：将所有子视图放置在屏幕的左上角（默认），并按顺序叠加。适用于堆叠布局，例如图片与文字叠加。
* **常用属性**：
  * `android:layout_gravity`：控制视图在布局中的对齐方式。

**示例**：

```xml
<FrameLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:src="@drawable/sample_image"/>
    
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Overlay Text"
        android:layout_gravity="center"/>
</FrameLayout>
```

#### 5. **GridLayout**

* **功能**：按网格排列子视图，可以指定每个视图在网格中的位置。
* **常用属性**：
  * `android:rowCount` 和 `android:columnCount`：设置行数和列数。
  * `android:layout_row` 和 `android:layout_column`：指定视图的行和列位置。

**示例**：

```xml
<GridLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:columnCount="2"
    android:rowCount="2">
    
    <Button
        android:text="Button 1"
        android:layout_row="0"
        android:layout_column="0"/>
    
    <Button
        android:text="Button 2"
        android:layout_row="0"
        android:layout_column="1"/>
    
    <Button
        android:text="Button 3"
        android:layout_row="1"
        android:layout_column="0"/>
    
    <Button
        android:text="Button 4"
        android:layout_row="1"
        android:layout_column="1"/>
</GridLayout>
```

#### 6. **TableLayout**

* **功能**：将子视图按表格的形式排列，适合用于表格数据布局。
* **常用属性**：
  * `android:stretchColumns`：定义哪些列可以被拉伸。

**示例**：

```xml
<TableLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
    
    <TableRow>
        <TextView android:text="Row 1, Column 1"/>
        <TextView android:text="Row 1, Column 2"/>
    </TableRow>
    
    <TableRow>
        <TextView android:text="Row 2, Column 1"/>
        <TextView android:text="Row 2, Column 2"/>
    </TableRow>
</TableLayout>
```

#### 总结

不同的布局管理器适用于不同的需求，选择合适的布局类型可以提高应用的灵活性和性能。安卓开发中常常会组合使用多种布局方式，以满足复杂的界面需求。
