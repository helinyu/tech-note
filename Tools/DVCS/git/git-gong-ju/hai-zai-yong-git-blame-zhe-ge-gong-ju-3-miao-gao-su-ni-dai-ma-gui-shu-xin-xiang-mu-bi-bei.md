# 还在用 git blame？这个工具3秒告诉你代码归属，新项目必备！



📌 \*\*一句话总结\*\*：\`git-who\` 是 \`git blame\` 的增强版，能让你快速搞清"这整块代码到底是谁写的？"



\---

在日常开发中，我们经常会遇到这样的场景：

\


\- 看到一段奇怪的逻辑，想问问谁写的？

\- 新接手一个项目，想知道有哪些人参与过开发？

\- Code Review 时想快速定位某段代码的历史作者？

\


这时候，很多人会想到 \`git blame\`。没错，它确实能告诉你每一行是谁最后修改的。但有没有更简洁、更直观的方式？

\


\*\*答案就是——\`git-who\`！\*\*

\


今天，我们就来聊聊这个"非官方但超实用"的 Git 小工具。

\


\---

\


\## 一、git-who 是什么？

\


首先明确一点：\`git-who\` 不是 Git 官方自带的命令，但它是一个\*\*真实存在的开源工具\*\*。

\


项目地址：https://github.com/sinclairtarget/git-who

\


\*\*核心特点\*\*：

\


\- \`git blame\` 告诉你\*\*每一行\*\*是谁写的

\- \`git-who\` 告诉你\*\*整个文件树\*\*是谁写的

\


简单来说，\`git-who\` 就像是 \`git blame\` 的"文件树版本"。

\


\### 举个🌰

\


假设你想知道 Python 解析器（Parser）目录下，哪些文件是谁写的：

\


\`\`\`bash

$ git who tree Parser/

Parser/.........................Guido van Rossum (182)

├── lexer/......................Pablo Galindo Salgado (5)

│   ├── buffer.c................Lysandros Nikolaou (1)

│   ├── lexer.h.................Lysandros Nikolaou (1)

│   └── state.h

├── tokenizer/..................Filipe Laíns (1)

│   ├── helpers.c...............Lysandros Nikolaou (1)

│   └── tokenizer.h.............Lysandros Nikolaou (1)

├── Python.asdl.................Benjamin Peterson (14)

├── parser.c....................Pablo Galindo Salgado (34)

└── pegen.c.....................Pablo Galindo (33)

\`\`\`

\


\*\*一眼就能看出\*\*：整个 Parser 目录主要是 Guido van Rossum 写的，但 lexer 子目录主要是 Pablo Galindo Salgado 负责的。

\


是不是比一行一行看 \`git blame\` 清晰多了？

\


\---

\


\## 二、git-who 的三大核心功能

\


\`git-who\` 提供了三个子命令，每个都解决不同的问题：

\


\### 1️⃣ \`table\` - 贡献者统计表（默认）

\


查看整个仓库或某个目录的贡献者排名：

\


\`\`\`bash

$ git who

┌─────────────────────────────────────────────────────┐

│Author                            Last Edit   Commits│

├─────────────────────────────────────────────────────┤

│Guido van Rossum                  2 mon. ago   11,213│

│Victor Stinner                    1 week ago    7,193│

│Fred Drake                        13 yr. ago    5,465│

│Georg Brandl                      1 year ago    5,294│

│Benjamin Peterson                 4 mon. ago    4,724│

│...3,026 more...                                     │

└─────────────────────────────────────────────────────┘

\`\`\`

\


\*\*常用场景\*\*：

\- 新加入项目，想快速了解团队贡献者

\- 想知道某个目录下谁贡献最多

\


\*\*高级用法\*\*：

\`\`\`bash

\# 只看某个目录

$ git who Tools/

\


\# 只看某个版本

$ git who v3.7.1

\


\# 只看某个版本范围

$ git who v3.10.9..v3.11.9

\


\# 按代码行数排序

$ git who -l

\


\# 按文件数排序

$ git who -f

\`\`\`

\


\### 2️⃣ \`tree\` - 文件树视图

\


以树形结构展示每个文件/目录的主要贡献者：

\


\`\`\`bash

$ git who tree src/

src/.........................Alice Developer (156)

├── utils/....................Bob Coder (42)

│   ├── helper.js............Bob Coder (15)

│   └── validator.js.........Alice Developer (8)

├── components/...............Charlie Tester (89)

│   ├── Button.js............Charlie Tester (23)

│   └── Modal.js.............Alice Developer (12)

└── main.js..................Alice Developer (45)

\`\`\`

\


\*\*常用场景\*\*：

\- 快速了解项目结构对应的负责人

\- 找到某个模块的主要维护者

\


\*\*高级用法\*\*：

\`\`\`bash

\# 显示所有文件（包括未标注的）

$ git who tree -a

\


\# 限制显示深度

$ git who tree -d 2

\


\# 按代码行数标注

$ git who tree -l

\`\`\`

\


\### 3️⃣ \`hist\` - 历史时间线

\


查看贡献历史的时间线，了解项目的发展历程：

\


\`\`\`bash

$ git who hist

1990 ┤ #                                     Guido van Rossum (105)

1991 ┤ ##                                    Guido van Rossum (445)

1992 ┤ ###                                   Guido van Rossum (606)

...

2020 ┤ ###---------                          Victor Stinner (524)

2021 ┤ ##----------                          Victor Stinner (260)

2022 ┤ ##-------------                       Victor Stinner (366)

2023 ┤ ###---------------                    Victor Stinner (556)

2024 ┤ ##-----------------                   Serhiy Storchaka (321)

\`\`\`

\


\*\*常用场景\*\*：

\- 了解项目的演进历史

\- 查看某个时间段的主要贡献者

\


\*\*高级用法\*\*：

\`\`\`bash

\# 只看某个目录的历史

$ git who hist src/

\


\# 只看某个版本之后的历史

$ git who hist v3.12.0..

\


\# 按代码行数显示

$ git who hist -l

\`\`\`

\


\---

\


\## 三、为什么推荐你用 git-who？

\


\| 优势 | 说明 |

\|------|------|

\| ✅ \*\*更宏观的视角\*\* | 不只是看单行代码，而是看整个模块/目录的贡献 |

\| ✅ \*\*可视化清晰\*\* | 树形结构一目了然，比 \`git blame\` 更直观 |

\| ✅ \*\*多种统计维度\*\* | 支持按提交数、代码行数、文件数等排序 |

\| ✅ \*\*时间线分析\*\* | \`hist\` 命令帮你了解项目演进历史 |

\| ✅ \*\*性能优化\*\* | 内置缓存机制，大项目也能快速响应 |

\


\*\*适用场景\*\*：

\


\- 🎯 新接手项目，快速了解代码结构

\- 🎯 Code Review 时定位模块负责人

\- 🎯 项目重构前，了解各模块的贡献者

\- 🎯 团队管理，了解成员贡献分布

\


\---

\


\## 四、安装 git-who（3 种方式）

\


\### 方式 1：Mac 用户（最简单）

\


\`\`\`bash

$ brew install git-who

\`\`\`

\


\### 方式 2：下载预编译二进制

\


访问 \[GitHub Releases]\(https://github.com/sinclairtarget/git-who/releases)，下载对应系统的二进制文件。

\


\*\*Linux/macOS\*\*：

\`\`\`bash

\# 下载并解压

$ wget https://github.com/sinclairtarget/git-who/releases/download/v1.2/git-who-v1.2-linux-amd64.tar.gz

$ tar -xzf git-who-v1.2-linux-amd64.tar.gz

\


\# 移动到 PATH

$ sudo mv git-who /usr/local/bin/

\`\`\`

\


\*\*Windows\*\*：

下载 \`.exe\` 文件，放到 PATH 环境变量中的目录即可。

\


\### 方式 3：Go 用户（源码安装）

\


\`\`\`bash

$ go install github.com/sinclairtarget/git-who@latest

\`\`\`

\


\### 方式 4：Docker（无需安装）

\


\`\`\`bash

\# 直接运行

$ docker run --rm -it -v "$(pwd)":/git git-who who

\


\# 或者设置 Git 别名

$ git config --global alias.who '!docker run --rm -it -v$(pwd):/git git-who who'

\`\`\`

\


\---

\


\## 五、快速上手：5 分钟实战

\


\### 步骤 1：安装（选择上面任一方式）

\


\`\`\`bash

$ brew install git-who  # Mac 用户推荐

\`\`\`

\


\### 步骤 2：验证安装

\


\`\`\`bash

$ git who --version

git-who version 1.2

\`\`\`

\


\### 步骤 3：查看项目贡献者

\


\`\`\`bash

\# 进入任意 Git 仓库

$ cd your-project

\


\# 查看所有贡献者

$ git who

\


\# 查看某个目录的贡献者

$ git who src/

\


\# 查看文件树

$ git who tree src/

\`\`\`

\


\### 步骤 4：探索高级功能

\


\`\`\`bash

\# 按代码行数排序

$ git who -l

\


\# 查看历史时间线

$ git who hist

\


\# 只看最近 3 个月的贡献

$ git who --since "3 months ago"

\`\`\`

\


\---

\


\## 六、实用技巧 & 进阶用法

\


\### 技巧 1：过滤特定作者

\


\`\`\`bash

\# 只看某个作者的贡献

$ git who --author "Alice Developer"

\


\# 排除某个作者

$ git who --nauthor "Bot User"

\`\`\`

\


\### 技巧 2：时间范围过滤

\


\`\`\`bash

\# 只看最近 6 个月的贡献

$ git who --since "6 months ago"

\


\# 只看某个时间段

$ git who --since "2024-01-01" --until "2024-12-31"

\`\`\`

\


\### 技巧 3：排除特定文件类型

\


\`\`\`bash

\# 排除 .c 文件

$ git who tree -- Parser/ ':!\*.c'

\


\# 排除测试文件

$ git who tree -- src/ ':!\*test\*'

\`\`\`

\


\### 技巧 4：结合 Git 别名

\


\`\`\`bash

\# 添加到 \~/.gitconfig

\[alias]

&#x20;   who-tree = "!git who tree"

&#x20;   who-hist = "!git who hist"

&#x20;   who-stats = "!git who -l"

\`\`\`

\


\### 技巧 5：禁用缓存（调试用）

\


\`\`\`bash

\# 如果结果不对，可以禁用缓存重新计算

$ GIT\_WHO\_DISABLE\_CACHE=1 git who

\`\`\`

\


\---

\


\## 七、git-who vs git blame：什么时候用哪个？

\


\| 场景 | 推荐工具 | 原因 |

\|------|---------|------|

\| 想知道某行代码是谁写的 | \`git blame\` | 精确到行级别 |

\| 想知道整个模块是谁写的 | \`git-who tree\` | 文件树级别，更宏观 |

\| 想了解项目贡献者排名 | \`git-who table\` | 统计表清晰直观 |

\| 想了解项目演进历史 | \`git-who hist\` | 时间线视图 |

\| 新接手项目，快速了解结构 | \`git-who tree\` | 一目了然 |

\


\*\*最佳实践\*\*：

\


\- 🔍 \*\*定位具体问题\*\* → 用 \`git blame\`

\- 📊 \*\*了解整体情况\*\* → 用 \`git-who\`

\- 🕐 \*\*分析历史演进\*\* → 用 \`git-who hist\`

\


\---

\


\## 八、常见问题 FAQ

\


\### Q1：git-who 会影响 Git 仓库吗？

\


\*\*A\*\*：完全不会！\`git-who\` 是只读工具，只读取 Git 历史，不会修改任何内容。

\


\### Q2：大项目会很慢吗？

\


\*\*A\*\*：\`git-who\` 内置了缓存机制，第一次运行会慢一些，后续会很快。如果觉得慢，可以设置 \`GIT\_WHO\_DISABLE\_CACHE=1\` 禁用缓存（但会更慢）。

\


\### Q3：支持 Git mailmap 吗？

\


\*\*A\*\*：支持！如果你的仓库有 \`.mailmap\` 文件，\`git-who\` 会自动识别，合并同一个人的不同邮箱/名字。

\


\### Q4：可以忽略某些提交吗？

\


\*\*A\*\*：可以！在仓库根目录创建 \`.git-blame-ignore-revs\` 文件，列出要忽略的提交哈希，\`git-who\` 会自动跳过。

\


\### Q5：Windows 能用吗？

\


\*\*A\*\*：可以！从 \[GitHub Releases]\(https://github.com/sinclairtarget/git-who/releases) 下载 Windows 版本即可。

\


\---

\


\## 九、结语 & 互动

\


\`git-who\` 虽然是个"小工具"，但用好了，能让你在团队协作中事半功倍。

\


\*\*记住\*\*：

\- ✅ 宏观视角用 \`git-who\`

\- ✅ 微观定位用 \`git blame\`

\- ✅ 两者结合，效率翻倍

\


\---

\


\### 📌 小调查

\


你平时用 \`git blame\` 多吗？有没有遇到过"这代码谁写的？"的灵魂拷问？

\


\*\*欢迎在评论区分享你的 Git 使用心得！\*\*

\


\---

\


\### 🔗 延伸阅读

\


\- \[Git 官方文档：git-blame]\(https://git-scm.com/docs/git-blame)

\- \[git-who 项目地址]\(https://github.com/sinclairtarget/git-who)

\- \[Git mailmap 文档]\(https://git-scm.com/docs/gitmailmap)

\


\---

\


\### ✨ 关注我们

\


如果你喜欢这类实用开发技巧，欢迎\*\*点赞、转发\*\*，并关注本公众号「\*\*技术小难\*\*」，每周分享一个提升生产力的小工具！

\


\---
