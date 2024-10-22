# event.stopPropagation() vs event.preventDefault()

`event.stopPropagation()` 和 `event.preventDefault()` 是 JavaScript 中两个重要的事件处理方法，它们在事件管理中扮演着不同的角色。下面是对这两个方法的详细对比：

#### 1. 定义

* **`event.stopPropagation()`**:
  * 阻止事件从目标元素向上传播到其父元素。
  * 使用场景：在嵌套元素中，防止父元素的事件处理程序被触发。
* **`event.preventDefault()`**:
  * 阻止事件的默认行为（如链接跳转、表单提交等）。
  * 使用场景：在需要拦截默认行为时，如防止链接导航或表单提交。

#### 2. 影响

| 方法                        | 事件传播    | 默认行为   |
| ------------------------- | ------- | ------ |
| `event.stopPropagation()` | 阻止事件冒泡  | 不影响    |
| `event.preventDefault()`  | 不影响事件传播 | 阻止默认行为 |

#### 3. 示例代码

**`event.stopPropagation()`**

```html
<div id="parent" style="padding: 20px; border: 1px solid black;">
    <button id="child">点击我</button>
</div>

<script>
    document.getElementById('parent').addEventListener('click', function() {
        console.log('父元素被点击');
    });

    document.getElementById('child').addEventListener('click', function(event) {
        console.log('子元素被点击');
        event.stopPropagation(); // 阻止事件冒泡
    });
</script>
```

**输出：**

*   点击子元素（按钮）：

    ```
    子元素被点击
    ```

**`event.preventDefault()`**

```html
<a href="https://example.com" id="link">点击我</a>

<script>
    document.getElementById('link').addEventListener('click', function(event) {
        console.log('链接被点击');
        event.preventDefault(); // 阻止默认行为（链接导航）
    });
</script>
```

**输出：**

*   点击链接：

    ```
    链接被点击
    ```
* 不会导航到 `https://example.com`。

#### 4. 组合使用

这两个方法可以结合使用，分别处理事件传播和默认行为。例如：

```html
<form id="form">
    <button type="submit">提交</button>
</form>

<script>
    document.getElementById('form').addEventListener('submit', function(event) {
        console.log('表单被提交');
        event.preventDefault(); // 阻止表单提交的默认行为
        // 这里可以处理自定义的提交逻辑
    });
</script>
```

#### 5. 总结

* **`event.stopPropagation()`**: 主要用于控制事件传播，防止上层元素的事件处理程序被触发。
* **`event.preventDefault()`**: 主要用于拦截和阻止默认的浏览器行为。

理解这两个方法的作用和使用场景，可以帮助开发者更好地管理用户交互，提高应用的可控性和用户体验。
