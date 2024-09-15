# 模板

在 Python 中通常所说的“模板”可能有以下几种含义：

**一、字符串模板（`string.Template`）**

Python 的 `string` 模块中有 `Template` 类，用于进行简单的字符串替换操作。

例如：

```python
from string import Template

s = Template('Hello, $name!')
print(s.substitute(name='Alice'))
```

**二、网页模板（如 Jinja2）**

在 Web 开发中，常使用模板引擎来生成动态网页。Jinja2 是一个广泛使用的 Python 模板引擎。它允许在 HTML 等文件中定义模板，其中包含变量和控制结构，然后通过传入具体的数据来渲染生成最终的网页内容。

例如：

```html
<!-- template.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

使用 Python 代码来渲染这个模板：

```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader('.'))
template = env.get_template('template.html')
rendered_html = template.render(name='Bob')
print(rendered_html)
```

**三、代码模板（开发工具中的模板）**

在一些集成开发环境（IDE）或代码编辑器中，可以定义代码模板。例如，在输入特定的关键字后，IDE 会自动展开为一段预设的代码结构，以提高开发效率。比如在 PyCharm 中，可以自定义代码片段模板。
