# 设置submodule子模块

{% hint style="info" %}
`submodule` 是一种将一个Git仓库嵌套在另一个Git仓库中的方式，适用于项目之间的依赖关系。

Git 子模块可以帮助你管理项目间的依赖，**保证子项目与主项目的版本同步**。
{% endhint %}

#### 1. 添加 Submodule

假设你有一个主项目（主仓库），并且要将一个子项目（子仓库）作为子模块添加到主项目中。

```bash
git submodule add <子项目的Git仓库URL> <子模块路径>
```

举个例子：

```bash
git submodule add https://github.com/example/other-project.git libs/other-project
```

这样就会把 `other-project` 仓库作为子模块添加到主项目的 `libs/other-project` 目录下。

#### 2. 初始化和更新 Submodule

如果你克隆了包含子模块的仓库，或者其他开发者第一次拉取代码，他们需要初始化并更新子模块。可以通过以下命令来完成这两个步骤：

```bash
git submodule init
git submodule update
```

或者使用以下命令同时完成初始化和更新操作：

```bash
git submodule update --init --recursive
```

#### 3. 在子模块中进行修改

如果你需要在子模块中进行修改，进入子模块目录并像平常一样进行开发：

```bash
cd libs/other-project
# 进行修改和提交
git commit -am "修改子模块"
git push
```

#### 4. 主项目更新子模块引用

每次修改完子模块之后，主项目需要记录子模块的新的提交引用。回到主项目目录，使用以下命令来提交更新的子模块引用：

```bash
cd ..
git add libs/other-project
git commit -m "更新子模块引用"
git push
```

#### 5. 更新 Submodule（拉取更新）

如果子模块有更新，可以使用以下命令拉取最新的子模块内容：

```bash
git submodule update --remote
```

#### 6. 删除 Submodule

如果不再需要子模块，可以通过以下步骤删除：

1.  删除子模块目录：

    ```bash
    git submodule deinit -f <子模块路径>
    git rm -f <子模块路径>
    ```
2. 然后从 `.gitmodules` 文件中删除子模块的条目，并从 `.git/config` 中移除相关配置。
3.  最后，提交删除操作：

    ```bash
    git commit -m "删除子模块"
    ```
