# 多线程

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 执行耗时操作
    }
}

Thread thread = new Thread(new MyRunnable());
thread.start();
```

#### 3. **AsyncTask【过时了】**

* **使用方式**：Android 提供的一个异步任务类，适合执行短时间的后台操作。
* **优点**：简化了线程间的交互，可以直接更新 UI。
* **缺点**：已经在 Android 11 中被弃用，不推荐在新项目中使用。

```java
class MyAsyncTask extends AsyncTask<Void, Void, ResultType> {
    @Override
    protected ResultType doInBackground(Void... params) {
        // 执行耗时操作
        return result;
    }

    @Override
    protected void onPostExecute(ResultType result) {
        // 更新 UI
    }
}
```

#### 4. **Handler 和 Message**

* **使用方式**：通过 `Handler` 发送和接收消息，适合更新 UI 线程。
* **优点**：可以与 `Thread` 结合使用，便于在不同线程间传递消息和结果。
* **缺点**：代码相对复杂，需要处理 `Message` 对象。

```java
Handler handler = new Handler(Looper.getMainLooper()) {
    @Override
    public void handleMessage(Message msg) {
        // 处理消息，更新 UI
    }
};
```

#### 5. **Executor 和 ExecutorService**

* **使用方式**：使用 `Executors` 创建线程池，执行多线程任务。
* **优点**：更灵活的线程管理，适合处理多个短任务。
* **缺点**：需要更深入的线程管理知识。

```java
ExecutorService executorService = Executors.newFixedThreadPool(2);
executorService.execute(() -> {
    // 执行耗时操作
});
```

#### 6. **Kotlin 协程**

* **使用方式**：Kotlin 提供的轻量级协程，简化异步编程。
* **优点**：更简洁的语法，易于理解和维护，支持挂起函数，便于与 UI 线程交互。
* **缺点**：需要学习协程的基本概念。

```kotlin
GlobalScope.launch(Dispatchers.Main) {
    val result = withContext(Dispatchers.IO) {
        // 执行耗时操作
    }
    // 更新 UI
}
```

#### 小结

在 Android 开发中，多线程模型的选择取决于具体的需求和任务。对于简单的任务，可以使用 `Thread` 和 `Runnable`；对于需要频繁更新 UI 的任务，`Handler` 是个不错的选择；而对于复杂的异步任务，推荐使用 Kotlin 协程，它提供了更为直观和灵活的解决方案。