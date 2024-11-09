# becomeFirstResponder vs resignFirstResponder

在 iOS 开发中，`resignFirstResponder` 和 `becomeFirstResponder` 都是用于管理“第一响应者” (First Responder) 状态的方法，但它们的功能和作用相反。它们的主要区别如下：

#### 1. `becomeFirstResponder`

* **功能**：将当前对象设置为“第一响应者”。
* **用途**：通常用于需要接受用户输入的控件（如 `UITextField`、`UITextView` 等）。当一个控件成为第一响应者时，它就会获得焦点并且能够响应键盘事件或其他输入事件。
* **返回值**：返回一个布尔值（`BOOL`），表示是否成功成为第一响应者。如果当前对象已经是第一响应者或无法成为第一响应者（例如，控件被禁用或不可见），则返回 `NO`。
* **使用场景**：
  * 当你想要让某个输入框自动获得焦点并显示键盘时，可以调用 `becomeFirstResponder`。
  *   示例：

      ```objc
      [myTextField becomeFirstResponder];
      ```

#### 2. `resignFirstResponder`

* **功能**：将当前对象从“第一响应者”状态中移除。
* **用途**：通常用于释放输入控件的焦点，关闭键盘或停止响应输入事件。比如，用户完成输入后，键盘应当关闭，输入框应当失去焦点。
* **返回值**：返回一个布尔值（`BOOL`），表示是否成功放弃第一响应者身份。如果当前对象不是第一响应者，或者无法放弃第一响应者身份（例如，它被禁用或不可见），则返回 `NO`。
* **使用场景**：
  * 当用户完成输入并希望键盘消失时，可以调用 `resignFirstResponder`。
  *   示例：

      ```objc
      [myTextField resignFirstResponder];
      ```

#### 区别总结：

| 方法                     | 作用                       | 返回值                         | 使用场景             |
| ---------------------- | ------------------------ | --------------------------- | ---------------- |
| `becomeFirstResponder` | 使控件成为第一响应者，获得焦点并开始接受输入   | `BOOL`：成功返回 `YES`，失败返回 `NO` | 将控件设为焦点（例如，显示键盘） |
| `resignFirstResponder` | 使控件放弃第一响应者身份，失去焦点并停止接受输入 | `BOOL`：成功返回 `YES`，失败返回 `NO` | 放弃焦点，关闭键盘等       |

#### 实际使用场景：

1.  **获取焦点并弹出键盘**：

    ```objc
    [textField becomeFirstResponder]; // 让 textField 成为第一响应者，弹出键盘
    ```
2.  **放弃焦点并关闭键盘**：

    ```objc
    [textField resignFirstResponder]; // 让 textField 失去第一响应者身份，关闭键盘
    ```

#### 注意事项：

* 只有能够成为第一响应者的控件（如 `UITextField`、`UITextView`）才能调用 `becomeFirstResponder` 和 `resignFirstResponder`。
* 这些方法也常用于视图层次的键盘管理，尤其是在 `UIViewController` 中手动控制键盘的显示和隐藏。

总之，`becomeFirstResponder` 用于让一个控件成为第一响应者，`resignFirstResponder` 则用于让控件放弃第一响应者身份。
