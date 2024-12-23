# tree类工具

在 macOS 上，如果你需要类似 `tree` 的工具来可视化文件和目录结构，有以下几种选择：

#### 1. **安装 `tree` 工具**

通过 `Homebrew` 安装 `tree` 命令：

```bash
brew install tree
```

然后可以像在 Linux 中一样使用：

```bash
tree
tree -L 2  # 限制显示层级
```

#### 2. **使用内置命令 `find`**

macOS 自带 `find`，可以用以下命令替代 `tree` 的功能：

```bash
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'
```

#### 3. **`lsd`（ls 的增强版）**

`lsd` 是一个现代化的 `ls` 替代品，它支持树形输出：

```bash
brew install lsd
lsd --tree
```

#### 4. **`fd` + `bat` 组合**

如果你同时喜欢快速查找和树状输出，可以结合 `fd` 和 `bat`：

```bash
brew install fd bat
fd --type d | bat --paging=never
```

#### 5. **可视化工具**

* **Visual Studio Code** 的文件资源管理器。
