# Swagger UI + 服务器

要将 Swagger UI 与服务器结合，部署 API 文档供用户查看，下面是详细的操作步骤。假设你已经有了一个 OpenAPI 规范文档（通常是 `swagger.yaml` 或 `swagger.json` 文件），并且想要将这个文档展示为可交互的 API 文档页面。

#### 1. 准备工作

你需要以下工具和文件：

* **OpenAPI 规范文档**（例如 `swagger.yaml` 或 `swagger.json`）。
* **Web 服务器**：可以使用简单的静态文件服务器，或者用 Express、Nginx 等服务器托管 Swagger UI 和 OpenAPI 文档。

#### 2. 获取 Swagger UI

Swagger UI 是一个开源项目，它提供了一个漂亮且功能强大的用户界面来展示 OpenAPI 规范。你可以通过以下方式来获取和配置 Swagger UI。

**2.1 方法一：直接使用 CDN**

如果你不想自己下载 Swagger UI 文件，可以使用 Swagger UI 的 CDN。

1. 创建一个新的 `index.html` 文件，并插入以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>API Documentation</title>
  <!-- 引入Swagger UI的CSS样式 -->
  <link rel="stylesheet" type="text/css" href="https://unpkg.com/swagger-ui-dist@3.52.5/swagger-ui.css">
</head>
<body>
  <h1>API Documentation</h1>
  
  <!-- Swagger UI展示区域 -->
  <div id="swagger-ui"></div>

  <!-- 引入Swagger UI的JavaScript文件 -->
  <script src="https://unpkg.com/swagger-ui-dist@3.52.5/swagger-ui-bundle.js"></script>
  <script src="https://unpkg.com/swagger-ui-dist@3.52.5/swagger-ui-standalone-preset.js"></script>

  <!-- 配置Swagger UI -->
  <script>
    const ui = SwaggerUIBundle({
      url: "path_to_your_swagger_file/swagger.yaml",  // 指定OpenAPI文档的路径
      dom_id: '#swagger-ui',  // 在页面中显示Swagger UI的DOM元素ID
      deepLinking: true,  // 启用深度链接
      presets: [
        SwaggerUIBundle.presets.apis,  // 选择默认API接口展示样式
        SwaggerUIBundle.SwaggerUIStandalonePreset  // 启用独立的Swagger UI布局
      ],
      layout: "StandaloneLayout"  // 使用标准的单独布局
    });
  </script>
</body>
</html>
```

* 你需要把 `url: "path_to_your_swagger_file/swagger.yaml"` 替换为你的 OpenAPI 规范文件路径。这个文件可以是本地的 `.yaml` 或 `.json` 文件，或者是托管在 Web 服务器上的文件。

**2.2 方法二：下载并部署 Swagger UI**

如果你希望将 Swagger UI 文件放在本地服务器上，你可以按照以下步骤操作。

1. **下载 Swagger UI**

你可以从 [Swagger UI GitHub 仓库](https://github.com/swagger-api/swagger-ui) 下载 Swagger UI，或者使用 NPM 安装。

* 从 GitHub 克隆 Swagger UI：

```bash
git clone https://github.com/swagger-api/swagger-ui.git
```

* 或者通过 NPM 安装：

```bash
npm install swagger-ui-dist
```

2. **将 Swagger UI 放在 Web 服务器上**

假设你下载了 Swagger UI 文件，并将其放在 Web 服务器的一个目录中。你需要在 HTML 文件中引用这些文件。

3. **配置 HTML 文件**

与方法一类似，配置 HTML 文件来加载 Swagger UI：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>API Documentation</title>
  <link rel="stylesheet" type="text/css" href="swagger-ui.css"> <!-- 本地路径 -->
</head>
<body>
  <h1>API Documentation</h1>
  
  <div id="swagger-ui"></div>

  <script src="swagger-ui-bundle.js"></script> <!-- 本地路径 -->
  <script src="swagger-ui-standalone-preset.js"></script> <!-- 本地路径 -->

  <script>
    const ui = SwaggerUIBundle({
      url: "swagger.yaml",  // 指定OpenAPI文档的路径
      dom_id: '#swagger-ui',  // 在页面中显示Swagger UI的DOM元素ID
      deepLinking: true,  // 启用深度链接
      presets: [
        SwaggerUIBundle.presets.apis,
        SwaggerUIBundle.SwaggerUIStandalonePreset
      ],
      layout: "StandaloneLayout"
    });
  </script>
</body>
</html>
```

* `swagger.yaml` 是你实际存放 OpenAPI 文档的路径，可以是本地路径或通过 URL 访问的文件。

#### 3. 部署到 Web 服务器

**3.1 使用简单的静态文件服务器**

可以使用简单的静态文件服务器来托管上述 HTML 文件和 OpenAPI 文档。如果你已经安装了 **Python**，可以在终端中使用 Python 启动一个静态服务器。

1. 进入包含你的 `index.html` 和 `swagger.yaml` 文件的目录。
2. 运行以下命令启动一个静态文件服务器：

*   Python 2.x：

    ```bash
    python -m SimpleHTTPServer 8000
    ```
*   Python 3.x：

    ```bash
    python -m http.server 8000
    ```

然后，你可以在浏览器中访问 `http://localhost:8000`，就能看到 Swagger UI 展示你的 OpenAPI 文档。

**3.2 使用 Node.js 的 HTTP 服务器**

如果你更喜欢 Node.js，你可以使用 `http-server` 模块快速启动一个静态文件服务器。

1. 安装 `http-server`（如果还没有安装的话）：

```bash
npm install -g http-server
```

2. 进入你的项目目录，启动服务器：

```bash
http-server
```

这将默认在 `http://localhost:8080` 启动一个 HTTP 服务器。

**3.3 使用 Nginx 部署**

如果你使用 Nginx 来托管静态文件，可以将 Swagger UI 和你的 OpenAPI 文档放置到 Nginx 配置的目录中（例如 `/usr/share/nginx/html`）。然后通过配置 Nginx 来提供服务。

* 将 `index.html` 和 `swagger.yaml` 上传到 Nginx 的目录（如 `/usr/share/nginx/html`）。
* 配置 Nginx 的虚拟主机来访问这些文件。

Nginx 配置示例：

```nginx
server {
    listen 80;
    server_name your-api-docs.com;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }

    location /swagger.yaml {
        root /usr/share/nginx/html;
    }
}
```

重启 Nginx 服务：

```bash
sudo service nginx restart
```

然后，你可以在浏览器中访问 `http://your-api-docs.com` 查看 API 文档。

#### 4. 访问和使用

* 当一切部署完成后，访问你配置的 Web 地址（如 `http://localhost:8000` 或 `http://your-api-docs.com`），你将能够看到 Swagger UI 展示你的 OpenAPI 文档。
* 用户可以通过 Swagger UI 交互式地查看 API 接口、参数、响应等内容，还能发送请求测试接口。

#### 5. 自定义 Swagger UI

你还可以根据需要定制 Swagger UI 的外观和行为。Swagger UI 提供了多种配置选项，例如修改主题、添加授权信息、控制显示的 API 路径等。

如果你需要更复杂的自定义（比如添加额外的请求头或身份验证），可以通过修改 `SwaggerUIBundle` 配置对象来实现。

```javascript
const ui = SwaggerUIBundle({
  url: "swagger.yaml",  // OpenAPI文档路径
  dom_id: '#swagger-ui',
  deepLinking: true,
  presets: [SwaggerUIBundle.presets.apis],
  layout: "StandaloneLayout",
  authorizations: {
    api_key: {
      type: "apiKey",
      name: "X-API-KEY",
      in: "header"
    }
  }
});
```

#### 总结

1. **获取 Swagger UI**：你可以通过 CDN 引用、下载本地版本或通过 NPM 安装 Swagger UI。
2. **创建 HTML 文件**：配置 HTML 文件来加载 Swagger UI 和你的 OpenAPI 文档。
3. **部署到服务器**：可以使用静态文件服务器（如 Python、Node.js）或通过 Nginx 部署。
4. **访问 API 文档**：通过浏览器访问部署好的 Swagger UI，交互式查看和测试 API。
