# preventDefault

`event.preventDefault()` 是一个 JavaScript 方法，用于阻止浏览器执行事件的默认行为。这个方法常用于处理用户交互时，确保不会触发浏览器的默认响应，特别是在表单提交、链接导航等场景下。

#### 使用场景

以下是一些常见场景及其应用：

**1. 表单提交**

在处理表单提交事件时，通常会使用 `event.preventDefault()` 来防止表单的默认提交行为，这样可以实现自定义的处理逻辑，例如验证输入或使用 AJAX 提交数据。

```html
<form id="myForm">
    <input type="text" required>
    <input type="submit" value="提交">
</form>

<script>
    const form = document.getElementById('myForm');

    form.addEventListener('submit', function(event) {
        event.preventDefault(); // 阻止表单提交
        console.log('表单未提交，执行自定义操作');
    });
</script>
```

**2. 链接点击**

在处理链接点击事件时，可以使用 `event.preventDefault()` 阻止页面导航，以便执行自定义行为（如打开模态窗口或显示提示信息）。

```html
<a href="https://www.example.com" id="myLink">访问示例网站</a>

<script>
    const link = document.getElementById('myLink');

    link.addEventListener('click', function(event) {
        event.preventDefault(); // 阻止链接导航
        alert('链接被点击，但没有导航');
    });
</script>
```

**3. 按钮的默认行为**

对于某些按钮，如 `type="submit"` 的按钮，点击时会导致表单提交。使用 `event.preventDefault()` 可以防止这一行为，从而执行其他逻辑。

#### 如何使用

* **参数**：`event.preventDefault()` 没有参数。
* **调用方式**：通常在事件处理函数内调用，确保在事件触发时能正确阻止默认行为。

#### 注意事项

* **只阻止默认行为**：`event.preventDefault()` 只会阻止默认行为，不会阻止事件传播（如冒泡）。如果需要同时阻止事件传播，可以使用 `event.stopPropagation()`。
* **兼容性**：`event.preventDefault()` 在现代浏览器中广泛支持。对于旧版浏览器（如 IE8 及更早版本），可能需要使用 `return false` 来阻止默认行为和事件传播，但这并不是推荐的做法。

#### 总结

`event.preventDefault()` 是一个强大的方法，能够让开发者有效控制用户交互，避免触发不希望的默认行为。通过合理使用它，可以实现更流畅和定制化的用户体验。
