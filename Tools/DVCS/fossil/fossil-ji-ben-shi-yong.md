# fossil基本使用

Fossil 的命令行界面相对简单易用，许多命令与 Git 类似，但它也有独特的功能，如内置的 Wiki、问题跟踪等。以下是一些 Fossil 的常用命令及其用途：

#### 1. **仓库管理**

*   **创建一个新仓库**：

    ```bash
    fossil init repo-name.fossil
    ```

    这将创建一个名为 `repo-name.fossil` 的新仓库文件。
*   **打开（检出）仓库**：

    ```bash
    fossil open repo-name.fossil
    ```

    这将检出仓库，并创建一个工作目录供你进行开发。
*   **关闭仓库**：

    ```bash
    fossil close
    ```

    关闭当前的工作目录，不会删除文件，只是断开与仓库的关联。
*   **克隆远程仓库**：

    ```bash
    fossil clone https://url-to-repo repo-name.fossil
    ```

    从远程地址克隆一个 Fossil 仓库。
*   **检查仓库状态**：

    ```bash
    fossil status
    ```

    显示当前工作目录的状态，包括未提交的更改、文件等。

#### 2. **文件操作**

*   **添加新文件**：

    ```bash
    fossil add file-name
    ```

    添加新文件到版本控制中。
*   **删除文件**：

    ```bash
    fossil rm file-name
    ```

    将文件从版本控制中删除。
*   **忽略文件**： 创建或编辑 `.fossil-settings/ignore-glob` 文件，添加需要忽略的文件模式：

    ```bash
    *.log
    *.tmp
    ```

#### 3. **提交更改**

*   **查看更改的文件**：

    ```bash
    fossil changes
    ```

    显示所有已修改但未提交的文件。
*   **查看差异**：

    ```bash
    fossil diff
    ```

    显示工作目录中的文件更改与上次提交的差异。
*   **提交更改**：

    ```bash
    fossil commit -m "Commit message"
    ```

    提交当前更改，并附上提交信息。

#### 4. **历史和日志**

*   **查看提交历史**：

    ```bash
    fossil timeline
    ```

    查看仓库的提交历史，包括提交信息、时间等。
*   **查看特定文件的历史**：

    ```bash
    fossil finfo file-name
    ```

    显示特定文件的历史更改记录。
*   **查看提交详情**：

    ```bash
    fossil info commit-id
    ```

    查看特定提交的详细信息。

#### 5. **分支管理**

*   **查看所有分支**：

    ```bash
    fossil branch list
    ```

    显示所有分支。
*   **创建新分支**：

    ```bash
    fossil branch new branch-name current-branch
    ```

    创建一个新分支 `branch-name`，基于当前分支。
*   **切换到某个分支**：

    ```bash
    fossil update branch-name
    ```

    切换到 `branch-name` 分支。
*   **合并分支**：

    ```bash
    fossil merge branch-name
    ```

    将 `branch-name` 分支合并到当前分支。

#### 6. **同步和推送**

*   **同步远程仓库**：

    ```bash
    fossil sync
    ```

    与远程仓库同步，类似于 Git 中的 `git pull` 和 `git push`。
*   **推送更改到远程**：

    ```bash
    fossil push
    ```

    将本地提交推送到远程仓库。
*   **拉取远程更改**：

    ```bash
    fossil pull
    ```

    从远程仓库拉取最新的更改。

#### 7. **Web 界面**

*   **启动本地 Web 服务器**：

    ```bash
    fossil ui
    ```

    启动一个本地 Web 界面，默认情况下在浏览器中打开。
*   **绑定到特定端口**：

    ```bash
    fossil server --port 8080
    ```

    启动 Web 服务器并监听指定端口。

#### 8. **问题跟踪和 Wiki**

*   **查看问题列表**：

    ```bash
    fossil ticket list
    ```

    显示所有问题（tickets）。
*   **添加新问题**：

    ```bash
    fossil ticket create
    ```

    通过命令行或 Web UI 添加新问题。
*   **创建或编辑 Wiki 页面**：

    ```bash
    fossil wiki create page-name
    fossil wiki edit page-name
    ```

#### 9. **标签管理**

*   **给提交打标签**：

    ```bash
    fossil tag add tag-name commit-id
    ```

    给特定的提交添加标签。
*   **查看标签**：

    ```bash
    fossil tag list
    ```

    显示所有标签。

#### 10. **帮助命令**

*   **查看命令帮助**：

    ```bash
    fossil help
    ```

    显示所有可用命令。
*   **查看特定命令帮助**：

    ```bash
    fossil help command-name
    ```

    查看某个特定命令的详细帮助信息。

#### 总结

Fossil 的命令行工具非常直观，提供了项目管理所需的版本控制、分支管理、问题跟踪、Wiki 文档等功能。对于小型或中型项目，它的集成特性使得管理变得简单高效。
