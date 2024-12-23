# 更新仓库的同时更新子模块

要在使用 `git clone` 克隆一个 Git 仓库时，自动同时下载该仓库依赖的子模块（即子库），可以使用 `--recursive` 选项。这样可以确保你克隆仓库时不仅下载主仓库，还会自动下载所有依赖的子模块。

#### 克隆仓库并下载子模块

执行以下命令：

```bash
git clone --recursive <仓库URL>
```

例如，假设你要克隆的仓库 URL 为 `https://github.com/example/repo.git`，你可以使用以下命令：

```bash
git clone --recursive https://github.com/example/repo.git
```

#### 如果已经克隆仓库并且没有下载子模块

如果你已经克隆了仓库，但忘记使用 `--recursive` 参数，或者之后需要下载子模块，可以通过以下步骤来获取子模块：

1.  初始化子模块：

    ```bash
    git submodule init
    ```
2.  更新子模块：

    ```bash
    git submodule update
    ```
3.  如果你希望同时更新子模块及其内部的子模块（递归地），可以使用以下命令：

    ```bash
    git submodule update --init --recursive
    ```

#### 总结

* 使用 `git clone --recursive` 克隆仓库时会自动下载所有子模块。
* 如果已经克隆了仓库但没有使用 `--recursive`，可以使用 `git submodule init` 和 `git submodule update` 来手动下载子模块。
