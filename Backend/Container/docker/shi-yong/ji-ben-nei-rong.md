# 基本内容

Docker 是一个开源的容器化平台，用于开发、发布和运行应用程序。它通过将应用程序及其依赖项打包到一个轻量级、可移植的容器中，实现了跨环境的一致性和高效的资源利用率。以下是 Docker 入门指南：

***

### 1. **Docker 的核心概念**

#### - **镜像 (Image)**

镜像是一个只读模板，包含应用程序及其运行所需的环境和依赖。可以从官方或自定义镜像仓库中获取。

#### - **容器 (Container)**

容器是镜像的运行实例，具有独立的运行环境。容器是轻量级的，启动速度快。

#### - **仓库 (Registry)**

仓库用于存储和分发镜像。例如：

* **Docker Hub**：Docker 官方提供的公共仓库。
* **自建仓库**：使用工具如 Harbor。

***

### 2. **安装 Docker**

#### **步骤：**

1.  **Linux**（例如 Ubuntu）：

    ```bash
    sudo apt update
    sudo apt install docker.io
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
2. **Windows/Mac**：
   * 下载并安装 Docker Desktop。
   * 确保虚拟化已启用（Windows 需要启用 WSL2）。
3.  **验证安装**：

    ```bash
    docker --version
    ```

***

### 3. **常用命令**

#### **镜像操作**

*   搜索镜像：

    ```bash
    docker search <镜像名>
    ```
*   拉取镜像：

    ```bash
    docker pull <镜像名>
    ```
*   查看本地镜像：

    ```bash
    docker images
    ```

#### **容器操作**

*   启动容器：

    ```bash
    docker run -it <镜像名> /bin/bash
    ```
*   查看运行中的容器：

    ```bash
    docker ps
    ```
*   查看所有容器：

    ```bash
    docker ps -a
    ```
*   停止容器：

    ```bash
    docker stop <容器ID>
    ```
*   删除容器：

    ```bash
    docker rm <容器ID>
    ```

#### **其他命令**

*   查看 Docker 信息：

    ```bash
    docker info
    ```
*   清理未使用的资源：

    ```bash
    docker system prune
    ```

***

### 4. **创建简单的容器**

#### 示例：运行一个 Nginx 容器

1.  拉取镜像：

    ```bash
    docker pull nginx
    ```
2.  运行容器：

    ```bash
    docker run -d -p 8080:80 nginx
    ```
3. 打开浏览器访问 `http://localhost:8080`，你应该能看到 Nginx 的欢迎页面。

***

### 5. **Dockerfile 简介**

Dockerfile 是构建镜像的脚本文件，包含一系列指令。\
示例：

```Dockerfile
# 使用基础镜像
FROM ubuntu:20.04

# 安装软件包
RUN apt-get update && apt-get install -y nginx

# 设置容器启动命令
CMD ["nginx", "-g", "daemon off;"]
```

使用 Dockerfile 构建镜像：

```bash
docker build -t my-nginx .
```

***

### 6. **Docker Compose**

Docker Compose 用于管理多个容器的部署，使用 YAML 文件定义服务。\
示例 `docker-compose.yml`：

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  app:
    image: my-app
```

运行：

```bash
docker-compose up
```

***

### 7. **下一步学习方向 【预留以后学习】**

* **深入理解网络、存储、卷（Volumes）**
* **学习如何构建和优化自定义镜像**
* **学习 Kubernetes（容器编排工具）**
* **探索 CI/CD 与 Docker 的结合**
