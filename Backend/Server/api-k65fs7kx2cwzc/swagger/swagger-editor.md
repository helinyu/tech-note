# Swagger Editor

### 1、官方已经提供了线上编辑地址：

&#x20;[https://editor.swagger.io/](https://editor.swagger.io/)



### 2、自己部署

**Swagger Editor** 是一个基于 Web 的 OpenAPI 编辑工具，它允许开发者编写、编辑、验证和查看 OpenAPI 规范的 API 文档。Swagger Editor 实际上是一个用 JavaScript 构建的前端应用，通常通过一个单独的容器来托管并运行。它的核心是一个基于浏览器的界面，用于创建和编辑 OpenAPI 文档，并且能够实时展示文档的效果。

#### 1. Swagger Editor 的构建原理

Swagger Editor 由以下几个主要部分组成：

**1.1 前端界面**

* **界面部分**：Swagger Editor 的前端界面通常由两个主要区域组成：
  * **编辑区域**：在这里，用户可以编写 OpenAPI 的 YAML 或 JSON 文件，定义 API 的路径、请求参数、响应等。
  * **预览区域**：在这个区域，用户可以实时查看 OpenAPI 文档的效果，文档会以交互式的格式展示出来。

**1.2 后端服务（可选）**

虽然 Swagger Editor 本身是一个前端应用，但如果你使用本地部署版本，它通常会有一个后端服务来托管文档，执行 OpenAPI 规范的验证和支持其他功能。

**1.3 Swagger Parser 和 Swagger UI**

* **Swagger Parser**：Swagger Editor 使用 `swagger-parser` 库来解析 OpenAPI 文档。这个库负责验证文档的有效性，确保其符合 OpenAPI 规范。
* **Swagger UI**：Swagger Editor 使用 Swagger UI 来渲染 OpenAPI 文档并展示给用户。Swagger UI 提供交互式文档展示，支持请求的模拟和查看接口的详细信息。

#### 2. Swagger Editor 工作流程

1. **加载 OpenAPI 文档**：用户打开 Swagger Editor 后，默认会有一个示例文档。用户可以通过界面直接修改文档内容（YAML 或 JSON 格式）。
2. **实时预览**：每当用户编辑文档时，Swagger Editor 会即时通过 `swagger-parser` 解析文档并验证其正确性。在编辑区域下方会显示文档的错误或警告。
3. **接口定义和描述**：用户定义 API 的路径、请求方法（GET、POST、PUT、DELETE等）、请求体、响应等。文档会实时更新，并在右侧显示相应的交互式 API 文档。
4. **导出和下载**：编辑完成后，用户可以将文档导出为 `.yaml` 或 `.json` 文件，或者通过 URL 分享给其他开发人员。

#### 3. Swagger Editor 的前端构建

Swagger Editor 的前端构建大致包括以下技术栈：

**3.1 使用 React 和其他前端框架**

Swagger Editor 的前端界面大部分是用 JavaScript（尤其是 React.js）构建的。React.js 提供了高效的 UI 渲染能力，而 Swagger UI 用于展示文档的交互式界面。

* **React**：用于构建编辑器的界面，并管理状态（比如文档内容、编辑器的变更）。
* **Monaco Editor**：Swagger Editor 使用 Monaco Editor 来实现编辑区域，Monaco 是一个高性能的代码编辑器，它是 Visual Studio Code 编辑器的核心部分。

**3.2 使用 Webpack 构建**

Swagger Editor 是通过 **Webpack** 构建的。Webpack 是一个现代化的 JavaScript 应用打包工具，它将前端资源（如 JavaScript、CSS、图片等）打包到一起，并优化性能。

**3.3 使用 Swagger UI 渲染 API 文档**

Swagger UI 负责将 OpenAPI 文档渲染为用户可以交互的 API 文档。Swagger UI 通过读取 Swagger JSON/YAML 文件，并将其显示为可操作的文档，用户可以看到各个 API 路径的详细信息，包括参数、响应示例、状态码等。

**3.4 基于 swagger-parser 进行 OpenAPI 文档验证**

Swagger Editor 使用 `swagger-parser` 库来验证 OpenAPI 文档的正确性。该库会检查文档的格式和内容是否符合 OpenAPI 规范，并在右侧面板中显示相关的错误或警告。

#### 4. Swagger Editor 的部署和构建

**4.1 使用 Docker 部署**

Swagger Editor 提供了 Docker 镜像，可以通过 Docker 快速启动 Swagger Editor。

**Docker 部署步骤**：

1. 拉取 Swagger Editor 镜像：

```bash
docker pull swaggerapi/swagger-editor
```

2. 运行 Docker 容器：

```bash
docker run -d -p 80:8080 swaggerapi/swagger-editor
```

这样就可以通过浏览器访问 Swagger Editor，默认访问地址是 `http://localhost`。

**4.2 使用 NPM 构建**

如果你希望从源代码构建 Swagger Editor，也可以按照以下步骤进行：

1. 克隆 Swagger Editor 的 GitHub 仓库：

```bash
git clone https://github.com/swagger-api/swagger-editor.git
```

2. 进入项目目录并安装依赖：

```bash
cd swagger-editor
npm install
```

3. 运行构建命令：

```bash
npm run start
```

这将会启动一个本地的开发环境，你可以在浏览器中访问 `http://localhost:3000` 查看 Swagger Editor。

#### 5. 如何自定义 Swagger Editor

你可以根据自己的需要对 Swagger Editor 进行一些自定义。例如：

* **定制主题**：你可以修改 Swagger UI 的主题，使其符合你的品牌风格。
* **插件支持**：你可以扩展 Swagger Editor，添加自定义插件来实现一些额外功能。
* **修改前端代码**：你也可以直接修改 React 和 Monaco 编辑器的代码，改变编辑器的行为或外观。

#### 6. Swagger Editor 使用实例

假设你有一个简单的 API，要定义如下的 API 路径：

* `/users`：GET 方法，返回所有用户。
* `/users/{id}`：GET 方法，返回特定用户的信息。

你可以在 Swagger Editor 中编写以下 OpenAPI 文档：

```yaml
openapi: 3.0.0
info:
  title: User API
  version: 1.0.0
  description: API for managing users
paths:
  /users:
    get:
      summary: Get all users
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
  /users/{id}:
    get:
      summary: Get a specific user
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: A specific user
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: integer
                  name:
                    type: string
```

#### 7. Swagger Editor 的优势和总结

* **实时预览和验证**：在编辑 OpenAPI 文档时，Swagger Editor 会实时验证并展示文档，确保文档的正确性。
* **易于使用**：Swagger Editor 提供了一个直观的用户界面，适合开发者快速编写和测试 API 文档。
* **开源**：Swagger Editor 是开源的，你可以自由定制或集成到你的项目中。
* **集成 Swagger UI**：可以直接将 Swagger UI 集成到 Swagger Editor 中，实时预览 API 文档。

通过 Swagger Editor，开发者可以更加高效地编写和管理 API 文档，并且为团队提供一个统一的 API 设计和测试平台。



