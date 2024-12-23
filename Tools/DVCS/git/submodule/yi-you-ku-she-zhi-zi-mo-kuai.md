# 已有库设置子模块

遇到这个错误是因为你尝试将 `third_lib/ReactiveSwift` 路径添加为子模块，但该路径已经存在于 Git 索引中。这可能是因为该目录已经被提交过文件，或者是该路径已经被跟踪过。

解决方法可以按照以下步骤：

#### 1. 确保该目录没有任何文件被跟踪

如果该目录之前已经存在文件，Git 会认为它已被跟踪。你需要先删除该目录中的文件或让 Git 停止跟踪它们。

```bash
# 确保删除该目录中的内容
rm -rf third_lib/ReactiveSwift
```

然后检查并清理 Git 索引：

```bash
git rm --cached third_lib/ReactiveSwift
```

这将从 Git 的索引中删除该目录，但不会删除本地文件。

#### 2. 添加子模块

现在你可以重新添加子模块了：

```bash
git submodule add git@github.com:ReactiveCocoa/ReactiveSwift.git third_lib/ReactiveSwift
```

#### 3. 提交更改

添加子模块后，提交更新：

```bash
git commit -m "添加 ReactiveSwift 子模块"
```

#### 4. 更新子模块

确保所有子模块初始化并更新：

```bash
git submodule update --init --recursive
```

#### 总结

这个错误通常是因为你尝试在已有内容的目录中添加子模块。通过先移除该目录的内容并清理 Git 索引，然后再重新添加子模块，你可以顺利完成操作。如果问题仍然存在，请检查是否有其他因素干扰 Git 的操作。
