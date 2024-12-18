# Swagger-ui

## 第一种方式：yaml 文件方式

#### 1、 创建一个目录test\_swagger&#x20;

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### 2、在目录下初始化，以及安装

```
npm init -y # 初始化
npm install express swagger-ui-express yamljs # 安装依赖库
```



#### 3、创建app.js

```
const express = require('express');
const swaggerUi = require('swagger-ui-express');
const YAML = require('yamljs');
const app = express();

// 加载OpenAPI文档
const swaggerDocument = YAML.load('./openapi.yaml');

// 设置Swagger UI
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));

// 启动应用
app.listen(3000, () => {
  console.log('API文档平台启动，访问 http://localhost:3000/api-docs');
});

```

4、创建openapi.yaml 文件

````
```yaml
openapi: 3.0.0
info:
  title: My API
  description: API documentation example
  version: 1.0.0
paths:
  /users:
    get:
      summary: Get all users
      description: Retrieves a list of users from the system
      responses:
        '200':
          description: A list of users
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    id:
                      type: integer
                    name:
                      type: string
  /users1:
    get:
      summary: Get all users
      description: Retrieves a list of users from the system
      responses:
        '200':
          description: A list of users
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    id:
                      type: integer
                    name:
                      type: string
```
````



#### 4、运行程序

执行命令： `node app.js`



## 第二种方式: json&#x20;

#### 1、将swagger UI 项目从github上clone下来 [https://github.com/swagger-api/swagger-ui](https://github.com/swagger-api/swagger-ui)

#### 2、将`dist`文件夹中的内容放到你的Web服务器上。

#### 3、创建一个`swagger.json`或`swagger.yaml`文件，放置在服务器上。

#### 4、配置`index.html`来加载你的OpenAPI文档，示例：

```
<!-- 在Swagger UI中加载你的OpenAPI文档 -->
<script>
  const ui = SwaggerUIBundle({
    url: "/path/to/your/openapi.json",  // 指定OpenAPI文档的路径
    dom_id: '#swagger-ui',
    deepLinking: true,
    presets: [
      SwaggerUIBundle.presets.apis,
      SwaggerUIBundle.SwaggerUIStandalonePreset
    ],
    layout: "StandaloneLayout"
  });
</script>

```

#### index.html 文件代码如下：

```
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

  <!-- 加载OpenAPI文档 -->
  <script>
    const ui = SwaggerUIBundle({
      url: "./openapi.json",  // 指定OpenAPI文档的路径
      dom_id: '#swagger-ui',  // 在页面中显示Swagger UI的DOM元素ID
      deepLinking: true,  // 启用深度链接
      presets: [
        SwaggerUIBundle.presets.apis,  // 选择默认API接口展示样式
        SwaggerUIBundle.SwaggerUIStandalonePreset  // 启用独立的Swagger UI布局
      ],
      // layout: "StandaloneLayout"  // 使用标准的单独布局
    });
  </script>
</body>
</html>

```
