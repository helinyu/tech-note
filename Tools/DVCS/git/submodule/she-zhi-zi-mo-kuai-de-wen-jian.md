# 设置子模块的文件

要查看当前 Git 项目中所有依赖的子模块（即子项目），可以使用以下命令：

#### 1. 查看 `.gitmodules` 文件

Git 会在项目根目录下自动生成一个 `.gitmodules` 文件，里面记录了所有子模块的信息，包括子模块的路径和仓库地址。你可以查看该文件来了解当前项目的所有子模块。

```bash
cat .gitmodules
```

输出示例：

```
[submodule "third_lib/ReactiveSwift"]
    path = third_lib/ReactiveSwift
    url = git@github.com:ReactiveCocoa/ReactiveSwift.git
```

#### 2. 使用 `git submodule` 命令

你还可以使用 `git submodule` 命令来列出当前项目中所有的子模块及其状态：

```bash
git submodule
```

或者使用更详细的命令，查看每个子模块的具体信息，包括其当前的提交（commit）状态：

```bash
git submodule status
```

输出示例：

```
c8a4f1d9ec7b5e7b9ed7e3e71dbf3d8991bfc7b3 third_lib/ReactiveSwift (heads/master)
```

这会显示每个子模块的当前提交 ID、路径和对应的分支。

#### 3. 查看所有子模块的状态和更新

如果你想更深入地了解每个子模块的详细信息，可以使用以下命令：

```bash
git submodule update --recursive --remote
```

这将更新所有子模块，并且递归地查看子模块中的子模块（如果有）。

#### 总结

* `.gitmodules` 文件包含了子模块的基本信息。
* `git submodule status` 可以列出所有子模块及其当前提交状态。
* 使用 `git submodule` 命令可以查看所有子模块的基本信息和状态。

这些方法应该能帮助你查看当前项目所依赖的子模块。如果还有其他问题，随时告诉我！
