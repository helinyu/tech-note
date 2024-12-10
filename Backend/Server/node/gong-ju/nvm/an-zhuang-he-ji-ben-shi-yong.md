# 安装和基本使用

NVM（Node Version Manager）是一个用于管理多个 Node.js 版本的工具，方便在不同的项目中使用不同的 Node.js 版本。下面是一些常见的 NVM 使用命令和步骤：

#### 安装 NVM

1.  **在 macOS 或 Linux 上安装 NVM：** 打开终端并运行以下命令：

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    ```

    或者：

    ```bash
    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    ```
2.  **安装完成后，重启终端，或者运行以下命令以使配置生效：**

    ```bash
    source ~/.bashrc    # 对于 bash
    source ~/.zshrc     # 对于 zsh
    ```
3.  **确认安装：**

    ```bash
    command -v nvm
    ```

    如果安装成功，会显示 `nvm`。

#### 使用 NVM 管理 Node.js 版本

1.  **查看可用的 Node.js 版本：**

    ```bash
    nvm ls-remote
    ```
2.  **安装 Node.js 版本：** 例如，要安装 Node.js 16.0.0：

    ```bash
    nvm install 16.0.0
    ```

    如果你想安装最新的 LTS（长期支持）版本：

    ```bash
    nvm install --lts
    ```
3.  **切换 Node.js 版本：** 安装了多个版本后，可以使用以下命令切换：

    ```bash
    nvm use 16.0.0
    ```

    或者使用 `lts`：

    ```bash
    nvm use --lts
    ```
4.  **查看当前使用的 Node.js 版本：**

    ```bash
    nvm current
    ```
5.  **列出已安装的 Node.js 版本：**

    ```bash
    nvm ls
    ```
6.  **卸载 Node.js 版本：**

    ```bash
    nvm uninstall 16.0.0
    ```
7.  **设置默认 Node.js 版本：** 如果你想设置某个版本为默认版本：

    ```bash
    nvm alias default 16.0.0
    ```

#### 其他常用命令

*   **切换到系统版本（如果系统有 Node.js）：**

    ```bash
    nvm use system
    ```
*   **查看帮助文档：**

    ```bash
    nvm --help
    ```

