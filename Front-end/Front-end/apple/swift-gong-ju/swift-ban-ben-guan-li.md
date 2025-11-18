# Swift版本管理

## Swiftly 使用指南

### 什么是 Swiftly？

**Swiftly** 是 Swift 官方团队开发的版本管理工具，用于安装、管理和切换 Swift 工具链。它支持 macOS 和主流 Linux 发行版。

#### 类比理解

如果你熟悉 Node.js，**Swiftly 类似于 nvm (Node Version Manager)**：

| Swift 生态                | Node.js 生态           |
| ----------------------- | -------------------- |
| `swiftly install 6.2.1` | `nvm install 18.0.0` |
| `swiftly use 6.2.1`     | `nvm use 18.0.0`     |
| `swiftly list`          | `nvm list`           |
| `.swift-version`        | `.nvmrc`             |

**主要特点**：

* ✅ 官方维护，功能完整
* ✅ 支持项目版本锁定（`.swift-version` 文件）
* ✅ 支持快照版本（snapshot）
* ✅ 自动管理环境变量和 PATH

### 安装

#### macOS

**一键安装**：

```bash
curl -O https://download.swift.org/swiftly/darwin/swiftly.pkg && \
installer -pkg swiftly.pkg -target CurrentUserHomeDirectory && \
~/.swiftly/bin/swiftly init --quiet-shell-followup && \
. "${SWIFTLY_HOME_DIR:-~/.swiftly}/env.sh" && \
hash -r
```

**手动配置环境变量**（如需要）：

```bash
# 添加到 ~/.zshrc 或 ~/.bash_profile
if [ -f "$HOME/.swiftly/env.sh" ]; then
    source "$HOME/.swiftly/env.sh"
fi
```

#### Linux

```bash
curl -O https://download.swift.org/swiftly/linux/swiftly-$(uname -m).tar.gz && \
tar zxf swiftly-$(uname -m).tar.gz && \
./swiftly init --quiet-shell-followup && \
. "${SWIFTLY_HOME_DIR:-~/.local/share/swiftly}/env.sh" && \
hash -r
```

#### 验证安装

```bash
swiftly --version  # 应显示版本号，如 1.1.0
```

### 基本使用

#### 常用命令

```bash
# 查看已安装的版本
swiftly list

# 查看可用的版本
swiftly list-available

# 安装最新稳定版
swiftly install latest

# 安装特定版本
swiftly install 6.2.1
swiftly install 6.2.1 --use  # 安装并立即使用

# 切换版本
swiftly use 6.2.1
swiftly use latest
swiftly use xcode  # macOS: 使用 Xcode 工具链

# 查看当前使用的版本
swiftly use

# 卸载版本
swiftly uninstall 6.2.1

# 更新 swiftly 自身
swiftly self-update
```

#### 项目版本管理

在项目根目录创建 `.swift-version` 文件：

```bash
echo "6.2.1" > .swift-version
```

进入项目目录时，swiftly 会自动切换到指定版本。

#### 快照版本

```bash
# 安装最新快照
swiftly install main-snapshot

# 安装特定日期的快照
swiftly install 5.7-snapshot-2022-06-20

# 使用快照版本
swiftly use main-snapshot
```

### 高级用法

#### 自定义临时目录

```bash
TMPDIR=/large/file/tmp/storage swiftly install latest
```

#### JSON 格式输出

```bash
swiftly list --format json
swiftly list-available --format json
```

#### 其他选项

```bash
# 自动确认，无需交互
swiftly install 6.2.1 --assume-yes

# 启用详细输出
swiftly install 6.2.1 --verbose

# 进度跟踪
swiftly install 6.2.1 --progress-file /path/to/progress.jsonl
```

### 常见问题

#### 1. 环境变量未生效

**问题**：新终端中 `swiftly` 命令不可用。

**解决方案**：

* 确保已将 swiftly 环境配置添加到 shell 配置文件（`.zshrc` 或 `.bash_profile`）
* 运行 `source ~/.zshrc` 重新加载配置
* 检查 `~/.swiftly/env.sh` 文件是否存在

#### 2. 版本切换不生效

**问题**：切换版本后 `swift --version` 仍显示旧版本。

**解决方案**：

* 运行 `hash -r` 清除命令缓存
* 检查 PATH 环境变量是否正确
* 确保 `.swift-version` 文件格式正确

#### 3. 与 Xcode 冲突

**问题**：macOS 上使用 Xcode 的 Swift 版本。

**解决方案**：

* 使用 `swiftly use xcode` 切换到 Xcode 工具链
* 或使用 `swiftly unlink` 取消管理，直接使用系统工具链

### 竞品对比

#### Swift 版本管理工具

| 工具           | 维护者  | 特点           | 推荐场景           |
| ------------ | ---- | ------------ | -------------- |
| **Swiftly**  | ✅ 官方 | 功能完整，官方支持    | **推荐：大多数场景**   |
| **Swiftenv** | ❌ 社区 | 简单易用，社区维护    | 偏好社区工具         |
| **ASDF**     | ❌ 社区 | 通用版本管理器      | 需要管理多种语言       |
| **Homebrew** | ❌ 社区 | macOS 包管理器   | 已使用 Homebrew   |
| **Xcode**    | ✅ 官方 | iOS/macOS 开发 | iOS/macOS 专用开发 |

#### 其他语言的类似工具

| 语言          | 工具          | 官方/社区 |
| ----------- | ----------- | ----- |
| **Swift**   | **Swiftly** | ✅ 官方  |
| **Rust**    | rustup      | ✅ 官方  |
| **Haskell** | ghcup       | ✅ 官方  |
| **Node.js** | nvm         | ❌ 社区  |
| **Python**  | pyenv       | ❌ 社区  |
| **Ruby**    | rbenv       | ❌ 社区  |
| **Java**    | SDKMAN      | ❌ 社区  |
| **通用**      | asdf        | ❌ 社区  |

**选择建议**：

* **单一语言开发**：使用该语言的专用工具（如 Swiftly、nvm、pyenv）
* **多语言开发**：考虑使用通用工具（如 asdf、SDKMAN）
* **官方工具优先**：如果语言有官方版本管理器，优先使用（如 Swiftly、rustup）

### 最佳实践

1. **项目版本锁定**：在项目根目录使用 `.swift-version` 文件锁定 Swift 版本
2. **定期更新**：定期运行 `swiftly self-update` 更新 swiftly 本身
3. **清理旧版本**：定期卸载不再使用的旧版本工具链，节省磁盘空间
4. **团队协作**：将 `.swift-version` 文件提交到版本控制系统，确保团队使用相同版本
5. **CI/CD 集成**：在 CI/CD 流程中使用 swiftly 安装指定版本的 Swift

### 命令速查表

| 命令                                | 说明            |
| --------------------------------- | ------------- |
| `swiftly --version`               | 显示 swiftly 版本 |
| `swiftly list`                    | 列出已安装的工具链     |
| `swiftly list-available`          | 列出可安装的工具链     |
| `swiftly install <version>`       | 安装指定版本        |
| `swiftly install latest`          | 安装最新稳定版       |
| `swiftly use <version>`           | 切换到指定版本       |
| `swiftly use`                     | 显示当前使用的版本     |
| `swiftly update <version>`        | 更新工具链         |
| `swiftly uninstall <version>`     | 卸载工具链         |
| `swiftly self-update`             | 更新 swiftly    |
| `swiftly run <version> <command>` | 使用指定版本运行命令    |
| `swiftly link`                    | 链接工具链管理       |
| `swiftly unlink`                  | 取消链接工具链管理     |

### 相关资源

* **Swift 官方网站**：https://www.swift.org
* **Swiftly 源码**：https://github.com/swiftlang/swiftly
* **Swift 下载页面**：https://www.swift.org/download/
* **Swiftenv GitHub**：https://github.com/kylef/swiftenv
* **ASDF GitHub**：https://github.com/asdf-vm/asdf

***

_Swiftly 是 Swift 开发者的必备工具，它简化了 Swift 工具链的管理，让版本切换变得轻松自如。_
