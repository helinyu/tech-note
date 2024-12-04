# Swagger Codegen

**Swagger Codegen** 是一个用于生成客户端、服务器端和 API 文档的工具，它能够从 OpenAPI 规范（以前是 Swagger）生成多种编程语言和框架的代码。Swagger Codegen 支持多种输出格式，包括 API 客户端、API 服务器端、API 模型和文档等。它是通过分析 OpenAPI 规范（例如 `swagger.json` 或 `swagger.yaml` 文件）来生成代码的工具。

#### 1. Swagger Codegen 简介

Swagger Codegen 的主要目标是自动生成代码框架，帮助开发者加速开发过程，减少手动编码工作。它支持生成的代码包括：

* **客户端代码**：为不同的编程语言（如 Java、Python、JavaScript 等）生成 API 客户端，帮助与后端接口进行交互。
* **服务器端代码**：生成用于实现 API 的服务器代码，支持多种框架（如 Spring、Express、Flask 等）。
* **API 模型**：生成 API 使用的模型类或数据结构（如 Java POJOs 或 Python 类）。
* **API 文档**：基于 OpenAPI 规范生成 API 文档。

#### 2. 安装 Swagger Codegen

**2.1 使用 Homebrew 安装（适用于 macOS 或 Linux）**

如果你使用 macOS 或 Linux，可以通过 Homebrew 安装 Swagger Codegen：

```bash
brew install swagger-codegen
```

**2.2 使用 Docker 安装**

Swagger Codegen 提供了官方的 Docker 镜像，可以通过 Docker 来运行它，而不需要在本地安装 Java 或其他依赖。

```bash
docker pull swaggerapi/swagger-codegen-cli
```

然后，使用以下命令启动 Docker 容器并运行 Swagger Codegen：

```bash
docker run --rm -v ${PWD}:/local swaggerapi/swagger-codegen-cli generate -i /local/swagger.yaml -l java -o /local/output
```

**2.3 使用 JAR 文件安装**

你也可以直接使用 JAR 文件来运行 Swagger Codegen：

1. 从 [Swagger Codegen GitHub Releases](https://github.com/swagger-api/swagger-codegen/releases) 下载最新的 `swagger-codegen-cli.jar` 文件。
2. 使用 Java 命令运行 Swagger Codegen：

```bash
java -jar swagger-codegen-cli.jar generate -i swagger.yaml -l java -o ./output
```

#### 3. 使用 Swagger Codegen 生成代码

**3.1 基本命令格式**

基本命令格式如下：

```bash
swagger-codegen generate -i <input-spec> -l <language> -o <output-dir>
```

* `-i <input-spec>`：输入的 OpenAPI 规范文件，可以是本地的 `.yaml` 或 `.json` 文件，或者是一个 URL。
* `-l <language>`：目标编程语言，支持多种语言（例如 Java、Python、Node.js、Go 等）。
* `-o <output-dir>`：输出目录，用于存放生成的代码。

例如，生成一个 **Java** 客户端代码的命令：

```bash
swagger-codegen generate -i swagger.yaml -l java -o ./java-client
```

**3.2 生成 API 服务器端代码**

如果你想生成服务器端代码，可以使用以下命令：

```bash
swagger-codegen generate -i swagger.yaml -l spring -o ./spring-server
```

上面的命令将会基于 Swagger/OpenAPI 规范生成一个 Spring Boot 服务器端项目。

**3.3 支持的编程语言和框架**

Swagger Codegen 支持多种编程语言和框架，常见的包括：

* **Java**（`-l java`、`-l spring`）
* **Python**（`-l python`）
* **JavaScript/Node.js**（`-l nodejs`）
* **C#**（`-l csharp`）
* **Go**（`-l go`）
* **Ruby**（`-l ruby`）
* **PHP**（`-l php`）
* **Scala**（`-l scala`）
* **Swift**（`-l swift`）
* **TypeScript**（`-l typescript`）
* **HTML/Markdown**（`-l html`、`-l markdown`）用于生成 API 文档。

**3.4 示例：生成 Java 客户端代码**

1. 假设你有一个 `swagger.yaml` 文件，定义了你的 API。
2. 运行以下命令生成 Java 客户端代码：

```bash
swagger-codegen generate -i swagger.yaml -l java -o ./java-client
```

3. 这将在 `./java-client` 目录下生成 Java 客户端代码。

**3.5 示例：生成 Node.js 服务器端代码**

1. 假设你有一个 `swagger.yaml` 文件，定义了 API。
2. 运行以下命令生成 Node.js 服务器端代码：

```bash
swagger-codegen generate -i swagger.yaml -l nodejs-server -o ./nodejs-server
```

3. 这将在 `./nodejs-server` 目录下生成 Node.js 服务器端代码。

#### 4. Swagger Codegen 的高级选项

Swagger Codegen 提供了许多选项来定制生成的代码，例如选择特定的模板、指定 API 的包名等。

**4.1 设置模板和配置**

Swagger Codegen 支持通过 **配置文件** 和 **模板** 来自定义生成的代码。你可以提供一个自定义的配置文件，用于定制生成代码的方式。例如，设置 `model` 包名、`api` 包名等。

例如：

```bash
swagger-codegen generate -i swagger.yaml -l java -o ./java-client -c config.json
```

`config.json` 配置文件的内容可以是：

```json
{
  "modelPackage": "com.example.models",
  "apiPackage": "com.example.api",
  "artifactId": "my-api-client"
}
```

**4.2 生成 API 文档**

如果你只需要生成 API 文档而不生成代码，可以使用以下命令：

```bash
swagger-codegen generate -i swagger.yaml -l html -o ./api-docs
```

这将在 `./api-docs` 目录下生成 HTML 格式的 API 文档。

**4.3 生成特定版本的代码**

你还可以通过 `-v` 参数来指定 Swagger Codegen 的版本。例如：

```bash
swagger-codegen generate -i swagger.yaml -l java -v 2.4.15 -o ./java-client
```

**4.4 选择库类型**

对于某些语言，Swagger Codegen 允许选择不同的客户端库类型。例如，在 Java 中，你可以选择使用 `okhttp`、`retrofit` 等不同的库：

```bash
swagger-codegen generate -i swagger.yaml -l java -o ./java-client --library okhttp-gson
```

#### 5. Swagger Codegen 的常见用途

1. **生成客户端代码**：从 OpenAPI 规范生成多种编程语言的 API 客户端，简化客户端开发。
2. **生成服务器代码**：基于 OpenAPI 规范，生成不同框架的 API 服务器端代码，节省后端开发时间。
3. **生成 API 文档**：生成完整的 API 文档（HTML、Markdown 格式等），便于团队和第三方开发者理解 API。
4. **API 模型类**：生成 API 使用的模型类，避免重复编写模型定义，保证一致性。

#### 6. 示例：如何生成和使用 Java 客户端

假设你有以下 `swagger.yaml` 文件：

```yaml
openapi: 3.0.0
info:
  title: User API
  version: 1.0.0
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
```

1. 运行 Swagger Codegen 生成 Java 客户端：

```bash
swagger-codegen generate -i swagger.yaml -l java -o ./java-client
```

2. 进入 `java-client` 目录：

```bash
cd java-client
```

3. 编译并使用生成的客户端代码来访问 API。

```java
import io.swagger.client.ApiClient;
import io.swagger.client.ApiException;
import io.swagger.client.api.UserApi;
import io.swagger.client.model.User;

import java.util.List;

public class Main {
    public static void main(String[] args) {
        ApiClient client = new ApiClient();
        client.setBasePath("http://localhost:8080");

        UserApi api = new UserApi(client);
        try {
            List<User> users = api.getUsers();
            for (User user : users) {
                System.out.println("User ID: " + user.getId());
                System.out.println("User Name: " + user.getName());
            }
        } catch (ApiException e) {
            e.printStackTrace();
        }
    }
}
```

通过这些步骤，你可以快速生成并使用 Swagger Codegen 生成的客户端代码来与 API 进行交互。

#### 7. 总结

Swagger Codegen 是一个强大的工具，可以帮助你从 OpenAPI 规范自动生成客户端、服务器端代码和 API 文档。通过命令行工具，你可以轻松地根据你的需求生成支持多种编程语言的代码，快速实现 API 集成，减少开发时间和工作量。
