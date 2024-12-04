# apiKey

这段代码：

```javascript
api_key: {
  type: "apiKey",
  name: "X-API-KEY",
  in: "header"
}
```

是 Swagger UI 配置中的一部分，专门用于定义 **API 身份验证** 机制。它用于告知 Swagger UI 如何通过 API 密钥（API Key）进行身份验证。这个配置项是通过 `authorizations` 属性传递给 Swagger UI 的，用于指定如何处理请求中的身份验证。

#### 详细解释：

1. **`type: "apiKey"`**：
   * 这表示身份验证方式是通过 API 密钥。`apiKey` 是 Swagger 支持的一种常见身份验证类型，用来在 HTTP 请求头、请求参数或 cookies 中传递 API 密钥。
2. **`name: "X-API-KEY"`**：
   * `name` 指定了 API 密钥的名称。`X-API-KEY` 是一个常见的 API 密钥名称。这个名称通常会作为 HTTP 请求的 header 中的一个字段名（或者查询参数、cookie），并包含密钥的值。
   * 在实际应用中，`X-API-KEY` 可能是由服务器要求的特定 header 名称。不同的 API 服务可能会使用不同的密钥名称，常见的有 `Authorization`、`Api-Key`、`X-API-KEY` 等。
3. **`in: "header"`**：
   * `in` 属性指定了 API 密钥的传递方式。在这里，`header` 表示 API 密钥将作为 HTTP 请求的 **Header** 传递。
   * 另外，`in` 可以有其他值，例如：
     * `query`：表示密钥通过 URL 的查询参数传递。
     * `header`：表示密钥通过 HTTP 请求头传递（如 `X-API-KEY`）。
     * `cookie`：表示密钥通过 HTTP 请求的 Cookie 传递。

#### 使用示例：

假设你有一个 API，要求客户端在每个请求中提供一个 API 密钥（例如 `X-API-KEY`）。你可以在 Swagger UI 中定义这个 API 密钥的传递方式，让用户知道如何提供它。具体步骤如下：

1.  **定义 API 密钥**：

    在 OpenAPI 规范文件中，你可以通过 `securityDefinitions` 或 `components.securitySchemes` 来定义 API 密钥的类型：

    ```yaml
    components:
      securitySchemes:
        api_key:
          type: apiKey
          in: header
          name: X-API-KEY
    ```
2.  **指定需要 API 密钥的操作**：

    然后，您可以为需要身份验证的 API 操作指定该密钥：

    ```yaml
    security:
      - api_key: []
    ```

    这将告诉 Swagger UI 在每个请求中都需要 `X-API-KEY` 作为认证信息。
3.  **Swagger UI 显示**：

    当你在 Swagger UI 中加载 API 文档时，Swagger UI 会自动为你提供一个输入框，允许用户输入 API 密钥。例如：

    * 如果你配置了 `X-API-KEY`，Swagger UI 会在界面上显示一个输入框，要求用户在请求头中输入 API 密钥。
    * 当用户输入正确的 API 密钥后，Swagger UI 会自动将密钥添加到每个 API 请求的请求头中。

#### 结论

这段代码用于配置 Swagger UI 如何处理 API 密钥认证。它告诉 Swagger UI，所有请求都应该使用名为 `X-API-KEY` 的密钥，这个密钥应该放在请求头中。通过这种方式，Swagger UI 可以让开发者和用户了解如何使用 API 密钥进行身份验证，并自动为请求添加适当的身份验证信息。
