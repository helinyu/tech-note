# worktree

\# Git Worktree 使用指南

\


\## 什么是 Git Worktree？

\


\*\*Git worktree\*\* 允许你在同一个 Git 仓库中同时检出多个工作目录。每个 worktree 都有自己独立的工作目录，但共享同一个 \`.git\` 仓库数据。

\


\## 主要优势

\


1\. \*\*并行开发\*\*：可以同时在多个分支上工作，无需频繁切换分支

2\. \*\*快速切换\*\*：避免切换分支时的文件操作开销

3\. \*\*测试方便\*\*：在一个 worktree 中运行测试，另一个继续开发

4\. \*\*代码审查\*\*：在单独的 worktree 中查看和测试 PR

\


\## 基本命令

\


\### 创建 Worktree

\


\`\`\`bash

\# 创建新的 worktree，检出指定分支

git worktree add \<path> \<branch>

\


\# 创建新的 worktree，并创建新分支

git worktree add \<path> -b \<new-branch>

\


\# 示例：在 ../myproject-feature 目录创建 feature 分支的 worktree

git worktree add ../myproject-feature feature

\


\# 示例：创建新分支并检出到新目录

git worktree add ../myproject-hotfix -b hotfix/critical-bug

\`\`\`

\


\### 列出所有 Worktree

\


\`\`\`bash

\# 列出所有 worktree

git worktree list

\


\# 详细格式输出

git worktree list --porcelain

\`\`\`

\


\### 删除 Worktree

\


\`\`\`bash

\# 删除 worktree（需要先手动删除工作目录，或使用 --force）

git worktree remove \<path>

\


\# 强制删除（即使有未提交的更改）

git worktree remove --force \<path>

\


\# 示例

git worktree remove ../myproject-feature

\`\`\`

\


\### 移动 Worktree

\


\`\`\`bash

\# 移动 worktree 到新位置

git worktree move \<old-path> \<new-path>

\


\# 示例

git worktree move ../old-location ../new-location

\`\`\`

\


\### 清理已删除的 Worktree 引用

\


\`\`\`bash

\# 清理已删除但仍有引用的 worktree

git worktree prune

\`\`\`

\


\## 实际使用场景

\


\### 场景 1：开发新功能的同时修复紧急 Bug

\


\`\`\`bash

\# 主目录：开发新功能

cd /path/to/project

git checkout feature/new-feature

\# 继续开发...

\


\# 创建新的 worktree 修复 bug

git worktree add ../project-hotfix hotfix/critical-bug

cd ../project-hotfix

\# 修复 bug 并提交

git commit -am "Fix critical bug"

git push origin hotfix/critical-bug

\`\`\`

\


\


\


\### 场景 2：同时查看多个 PR

\


\`\`\`bash

\# 查看多个 PR 分支

git worktree add ../pr-123 pr-123

git worktree add ../pr-456 pr-456

git worktree add ../pr-789 pr-789

\


\# 在不同终端窗口中分别进入这些目录进行测试

cd ../pr-123 && npm test

cd ../pr-456 && npm test

cd ../pr-789 && npm test

\`\`\`

\


\### 场景 3：在不同 worktree 中运行不同的构建/测试

\


\`\`\`bash

\# 主目录：开发

cd /path/to/project

git checkout develop

\


\# 测试目录：运行测试套件

git worktree add ../project-test test-branch

cd ../project-test

npm test  # 在测试 worktree 中运行测试

\


\# 构建目录：构建生产版本

git worktree add ../project-build release-branch

cd ../project-build

npm run build  # 在构建 worktree 中构建

\`\`\`

\


\### 场景 4：代码审查

\


\`\`\`bash

\# 创建审查分支的 worktree

git worktree add ../review-pr-123 pr-123

\


\# 在审查 worktree 中查看代码

cd ../review-pr-123

code .  # 用编辑器打开

npm test  # 运行测试验证

\`\`\`

\


\## 注意事项

\


1\. \*\*不能同时检出同一分支\*\*：不能在多个 worktree 中同时检出同一个分支

2\. \*\*共享 Git 数据\*\*：所有 worktree 共享同一个 \`.git\` 目录

3\. \*\*删除限制\*\*：删除 worktree 时，需要确保没有未提交的更改（或使用 \`--force\`）

4\. \*\*路径位置\*\*：worktree 路径通常放在主仓库目录之外

5\. \*\*子模块\*\*：如果仓库包含子模块，每个 worktree 都需要单独初始化子模块

\


\## 常用命令速查

\


\`\`\`bash

\# 创建

git worktree add \<path> \[\<branch>]           # 检出现有分支

git worktree add \<path> -b \<new-branch>      # 创建并检出新分支

\


\# 查看

git worktree list                             # 列出所有 worktree

git worktree list --porcelain                # 详细格式

\


\# 删除

git worktree remove \<path>                    # 删除 worktree

git worktree remove --force \<path>           # 强制删除

\


\# 移动

git worktree move \<old-path> \<new-path>      # 移动 worktree

\


\# 清理

git worktree prune                            # 清理已删除的引用

\`\`\`

\


\## 最佳实践

\


1\. \*\*命名规范\*\*：使用描述性的目录名，如 \`../project-feature-name\` 或 \`../project-pr-123\`

2\. \*\*定期清理\*\*：定期删除不再需要的 worktree，保持工作区整洁

3\. \*\*路径管理\*\*：将 worktree 放在主项目目录的父目录中，便于管理

4\. \*\*文档记录\*\*：在团队中记录 worktree 的使用规范，避免冲突

\


\## 相关资源

\


\- \[Git 官方文档 - git-worktree]\(https://git-scm.com/docs/git-worktree)

\- \[Git Worktree 教程]\(https://git-scm.com/docs/git-worktree)

\
