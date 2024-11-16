# 基本示例

下面是一个简单的 Docker 使用示例，从拉取镜像到运行容器，以及如何构建自己的镜像。

***

#### **示例 1：运行一个简单的 Nginx 容器**

1.  **拉取镜像**

    ```bash
    docker pull nginx
    ```

    这会从 Docker Hub 拉取最新的 Nginx 镜像。
2.  **运行容器**

    ```bash
    docker run -d -p 8080:80 nginx
    ```

    * `-d`：后台运行容器。
    * `-p 8080:80`：将主机的 8080 端口映射到容器的 80 端口。
3. **验证** 打开浏览器，访问 `http://localhost:8080`，你应该会看到 Nginx 的欢迎页面。
4.  **停止容器**

    ```bash
    docker ps
    ```

    找到容器的 ID 或名称，然后停止它：

    ```bash
    docker stop <容器ID>
    ```
5.  **删除容器**

    ```bash
    docker rm <容器ID>
    ```

***

#### **示例 2：使用自定义 HTML 文件运行 Nginx**

1.  **创建 HTML 文件** 新建一个目录 `my-nginx`，并在其中创建一个 `index.html` 文件：

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Welcome to My Nginx!</title>
    </head>
    <body>
        <h1>Hello, Docker!</h1>
    </body>
    </html>
    ```
2.  **运行 Nginx 容器并挂载目录**

    ```bash
    docker run -d -p 8080:80 -v $(pwd)/my-nginx:/usr/share/nginx/html nginx
    ```

    * `-v $(pwd)/my-nginx:/usr/share/nginx/html`：将当前目录下的 `my-nginx` 文件夹挂载到容器中 Nginx 默认的网页目录。
3. **验证** 打开浏览器，访问 `http://localhost:8080`，你会看到自定义的 HTML 页面。

***

#### **示例 3：构建自定义镜像**

1.  **创建 Dockerfile** 在一个新目录下，创建文件 `Dockerfile`：

    ```Dockerfile
    # 使用官方 Nginx 基础镜像
    FROM nginx:latest

    # 拷贝本地的 index.html 到容器内
    COPY index.html /usr/share/nginx/html/index.html
    ```
2.  **创建 HTML 文件** 在同一目录下，创建 `index.html` 文件：

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>My Custom Nginx</title>
    </head>
    <body>
        <h1>Hello from my custom Docker image!</h1>
    </body>
    </html>
    ```
3.  **构建镜像**

    ```bash
    docker build -t my-nginx .
    ```
4.  **运行容器**

    ```bash
    docker run -d -p 8080:80 my-nginx
    ```
5. **验证** 再次访问 `http://localhost:8080`，你将看到来自自定义镜像的 HTML 页面。

***

#### **示例 4：运行一个 Python 应用**

1.  **创建 Python 脚本** 在一个新目录下创建文件 `app.py`：

    ```python
    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def home():
        return "Hello, Dockerized Flask App!"

    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=5000)
    ```
2.  **创建 Dockerfile**

    ```Dockerfile
    # 使用 Python 基础镜像
    FROM python:3.9-slim

    # 设置工作目录
    WORKDIR /app

    # 复制文件到容器
    COPY app.py /app

    # 安装依赖
    RUN pip install flask

    # 暴露端口
    EXPOSE 5000

    # 设置启动命令
    CMD ["python", "app.py"]
    ```
3.  **构建镜像**

    ```bash
    docker build -t flask-app .
    ```
4.  **运行容器**

    ```bash
    docker run -d -p 5000:5000 flask-app
    ```
5. **验证** 打开浏览器，访问 `http://localhost:5000`，你会看到 Flask 应用返回的消息。



**注意：macOS**：镜像存储在 Docker Desktop 的内部虚拟机中，无法直接通过文件系统访问。





### 将自定义镜像推送到 Docker Hub 的过程包括以下步骤：

***

#### 1. **登录 Docker Hub**

确保已经在 Docker Hub 注册了账户。

在终端登录 Docker Hub：

```bash
docker login
```

输入用户名和密码完成登录。

***

#### 2. **为镜像打标签**

Docker Hub 上的镜像需要一个带有仓库名称的标签。假设你的 Docker Hub 用户名是 `yourusername`，镜像名为 `custom-image`，并且本地镜像的版本是 `1.0`。

首先查看本地镜像的名称和 ID：

```bash
docker images
```

然后为镜像打标签：

```bash
docker tag <IMAGE_ID> yourusername/custom-image:1.0
```

例如：

```bash
docker tag abc123 yourusername/custom-image:1.0
```

***

#### 3. **推送镜像到 Docker Hub**

将镜像推送到 Docker Hub：

```bash
docker push yourusername/custom-image:1.0
```

推送完成后，可以通过 Docker Hub 网站或命令行查看镜像是否上传成功：

```bash
docker search yourusername/custom-image
```

***

#### 4. **测试镜像**

其他人可以通过以下命令拉取并使用你的镜像：

```bash
docker pull yourusername/custom-image:1.0
```

然后运行镜像：

```bash
docker run yourusername/custom-image:1.0
```

***

#### 5. **管理和优化**

* **设为公开：** 确保镜像在 Docker Hub 中是公开的，这样其他人才能访问。如果是私有镜像，用户需要凭证才能拉取。
* **编写描述：** 在 Docker Hub 镜像页面中编写详细的使用说明，包括镜像的用途和用法示例。

***
