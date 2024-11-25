# 生命周期钩子方法内部实现内容

在 Android 开发中，各个生命周期方法（钩子方法）是管理资源、保存状态和处理逻辑的关键。以下是各生命周期方法的典型用途和建议的实现内容。

***

#### **1. `onCreate()`**

**触发时机：**

* `Activity` 第一次创建时调用，只调用一次。

**适合做的事情：**

1. **初始化界面：**
   * 设置布局文件（`setContentView()`）。
   * 初始化控件并绑定事件。
2. **初始化数据：**
   * 创建或加载必要的数据资源。
   * 获取从其他 `Activity` 或 `Fragment` 传递的数据（`Intent` 或 `Arguments`）。
3. **初始化全局逻辑：**
   * 设置 ViewModel、依赖注入（如 Hilt/Dagger）。
   * 注册全局广播接收器。

**示例代码：**

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // 初始化控件
    Button button = findViewById(R.id.button);
    button.setOnClickListener(v -> {
        // 按钮点击事件
    });

    // 初始化数据
    String data = getIntent().getStringExtra("key");

    // 初始化 ViewModel
    viewModel = new ViewModelProvider(this).get(MyViewModel.class);
}
```

***

#### **2. `onStart()`**

**触发时机：**

* 当 `Activity` 对用户可见时调用。
* 紧接 `onCreate()` 或 `onRestart()` 后调用。

**适合做的事情：**

1. **恢复界面相关数据：**
   * 启动 UI 动画或刷新界面内容。
2. **注册资源：**
   * 注册可能需要的资源或监听器（如 `BroadcastReceiver`、`ContentObserver`）。
3. **预加载逻辑：**
   * 准备用户可见的动态内容。

**示例代码：**

```java
@Override
protected void onStart() {
    super.onStart();
    // 注册广播接收器
    registerReceiver(myReceiver, new IntentFilter("MY_ACTION"));

    // 刷新动态数据
    loadDynamicContent();
}
```

***

#### **3. `onResume()`**

**触发时机：**

* `Activity` 进入前台，可与用户交互。

**适合做的事情：**

1. **开始交互逻辑：**
   * 启动动态内容更新（如摄像头预览、视频播放）。
   * 恢复动画、音效或实时数据更新。
2. **检查权限或状态：**
   * 检查用户权限、网络连接等。
3. **重新注册短期资源：**
   * 注册传感器监听或其他实时资源。

**示例代码：**

```java
@Override
protected void onResume() {
    super.onResume();
    // 启动摄像头预览
    camera.startPreview();

    // 开启传感器监听
    sensorManager.registerListener(sensorListener, accelerometer, SensorManager.SENSOR_DELAY_NORMAL);
}
```

***

#### **4. `onPause()`**

**触发时机：**

* `Activity` 失去焦点，但仍然可见（如弹出对话框）。

**适合做的事情：**

1. **暂停交互逻辑：**
   * 暂停动画、视频播放、计时器等。
2. **保存状态：**
   * 临时保存未提交的用户输入或应用状态。
3. **释放实时资源：**
   * 停止使用高耗能的资源（如摄像头、传感器）。

**示例代码：**

```java
@Override
protected void onPause() {
    super.onPause();
    // 暂停摄像头
    camera.stopPreview();

    // 停止传感器监听
    sensorManager.unregisterListener(sensorListener);

    // 保存未提交的数据
    editor.putString("draft", editText.getText().toString());
    editor.apply();
}
```

***

#### **5. `onStop()`**

**触发时机：**

* `Activity` 对用户完全不可见。
* 通常在切换到其他应用或界面时调用。

**适合做的事情：**

1. **释放 UI 资源：**
   * 停止加载图片或不再需要的后台任务。
2. **取消注册监听器：**
   * 注销广播接收器、数据观察者等。
3. **保存重要状态：**
   * 持久化保存用户数据（如草稿、进度）。

**示例代码：**

```java
@Override
protected void onStop() {
    super.onStop();
    // 注销广播
    unregisterReceiver(myReceiver);

    // 停止后台任务
    if (backgroundTask != null) {
        backgroundTask.cancel();
    }

    // 保存用户草稿
    saveDraftToDatabase();
}
```

***

#### **6. `onDestroy()`**

**触发时机：**

* `Activity` 被销毁时调用。
* 通常在用户退出页面或因内存不足销毁 `Activity` 时触发。

**适合做的事情：**

1. **清理资源：**
   * 释放内存、线程、对象引用。
2. **销毁全局对象：**
   * 销毁 `Handler`、关闭数据库连接。

**示例代码：**

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // 释放摄像头资源
    if (camera != null) {
        camera.release();
        camera = null;
    }

    // 清理全局引用，防止内存泄漏
    myHandler.removeCallbacksAndMessages(null);
}
```

***

#### **7. `onRestart()`**

**触发时机：**

* 从后台重新进入前台，紧接 `onStop()` 后调用。

**适合做的事情：**

1. **重新初始化短期数据：**
   * 恢复 UI 状态或重新加载临时数据。
2. **刷新界面：**
   * 更新可能发生变化的内容（如从后台切回后，重新检查数据变化）。

**示例代码：**

```java
@Override
protected void onRestart() {
    super.onRestart();
    // 重新加载用户数据
    refreshUserData();
}
```

***

#### **小结**

以下是各生命周期适合处理的核心任务：

| **生命周期方法**    | **建议做的事情**             |
| ------------- | ---------------------- |
| `onCreate()`  | 初始化界面、数据、逻辑，注册全局依赖。    |
| `onStart()`   | 恢复界面相关内容，注册长期资源。       |
| `onResume()`  | 开始交互逻辑，恢复动态内容，注册实时监听器。 |
| `onPause()`   | 暂停动态内容，保存临时数据，释放实时监听器。 |
| `onStop()`    | 释放长期资源，保存关键数据，停止后台任务。  |
| `onDestroy()` | 清理所有资源和引用，销毁全局对象。      |
| `onRestart()` | 恢复短期数据，刷新界面内容。         |

