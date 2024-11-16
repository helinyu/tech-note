# Docker Compose

#### **什么是 Docker Compose?**

Docker Compose 是一个用于定义和管理多容器 Docker 应用程序的工具。它允许开发者通过一个单一的配置文件（通常是 `docker-compose.yml`）描述应用程序中所有的服务及其依赖关系，然后通过简单的命令对这些服务进行管理。

***

#### **主要功能**

1. **多容器管理**\
   Docker Compose 能够管理一个应用中多个相互依赖的容器（如 Web 服务、数据库、缓存等），将它们作为一个整体进行部署和维护。
2. **声明式配置**\
   使用 `docker-compose.yml` 文件以声明式的方式定义服务、网络、卷和其他设置，方便版本控制和团队协作。
3. **命令式操作**\
   提供简单的命令（如 `up`, `down`, `ps` 等）来启动、停止、重启服务。
4. **网络和数据管理**\
   自动为服务创建独立的网络和持久化存储卷，简化配置。
5. **环境隔离**\
   每个 Docker Compose 项目会运行在独立的环境中，不会干扰其他项目。

***

#### **典型工作流程**

**1. 创建 `docker-compose.yml` 文件**

描述应用中的服务及其依赖，例如：

```yaml
version: '3.8'

services:
  web:
    image: nginx
    ports:
      - "80:80"

  database:
    image: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
```

**2. 启动服务**

使用 `docker compose up` 命令启动服务：

```bash
docker compose up
```

加上 `-d` 参数可以后台运行：

```bash
docker compose up -d
```

**3. 查看运行中的服务**

使用以下命令查看服务状态：

```bash
docker compose ps
```

**4. 停止服务**

停止并清理容器、网络等：

```bash
docker compose down
```

***

#### **优点**

* **简单高效**：通过一个配置文件和一条命令即可管理多容器应用。
* **跨环境一致性**：开发、测试和生产环境可以使用相同的 Compose 文件，确保一致性。
* **易于维护**：所有服务及其配置集中在一个文件中，方便维护和团队协作。

***

#### **适用场景**

* **开发环境**：快速搭建复杂应用的开发环境（如 Web 应用 + 数据库 + 缓存）。
* **测试环境**：在容器中运行自动化测试。
* **小型生产环境**：部署小型、多容器的应用。
* **CI/CD 工作流**：在持续集成或交付管道中用来管理依赖的服务。

***

#### **与 Docker 的关系**

Docker Compose 是 Docker 的官方工具之一，与 `docker` CLI 相辅相成：

* Docker CLI 用于管理单个容器。
* Docker Compose 用于管理多个容器及其依赖的服务。

通过 Docker Compose，可以更轻松地管理微服务架构或多容器应用程序。
