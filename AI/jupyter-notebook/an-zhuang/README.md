# 安装

#### 1. 确保正确安装

* 重新下载安装包，并确保下载的是最新版本的 Anaconda。选择适合你操作系统的版本。

#### 2. 使用 Terminal

如果没有 GUI，你仍然可以通过 Terminal 使用 Jupyter Notebook：

**a. 打开 Terminal**

* 使用 Spotlight（按下 `Command + Space`）搜索并打开 Terminal。

**b. 创建 Anaconda 环境（可选）**

你可以创建一个新的环境来管理不同的库和依赖：

```bash
conda create --name 【名字jupyter_notebook】 python=3.11
```

然后激活环境：

```bash
conda activate jupyter_notebook
```

**c. 安装 Jupyter Notebook**

确保在你当前的 Anaconda 环境中安装 Jupyter Notebook：

```bash
conda install jupyter
```

**d. 启动 Jupyter Notebook**

在 Terminal 中输入：

```bash
jupyter notebook
```

这将启动 Jupyter Notebook 服务器，并在浏览器中打开界面。

#### 3. 使用 JupyterLab（可选）

如果你更喜欢更现代的界面，可以尝试 JupyterLab：

```bash
conda install jupyterlab
```

然后通过以下命令启动：

```bash
jupyter lab
```

#### 4. 检查 Anaconda 安装

如果问题依然存在，可以尝试重新安装 Anaconda，确保在安装过程中选择添加到 PATH 环境变量。

