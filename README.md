# 在终端中优雅地查看与管理 Markdown：Glow、Glamour 与 mdx/mdt

\


\# 在终端中优雅地查看与管理 Markdown：Glow、Glamour 与 mdx/mdt

\


\## 一、前言

在终端中处理 Markdown 文件是开发者的日常操作之一。过去我们通常依赖 \`cat\` 或 \`less\` 来查看，但这些工具并不能高亮渲染 Markdown 样式。\`Glow\` 和 \`Glamour\` 的出现，让 Markdown 在命令行中也能拥有类似网页端的阅读体验。

\


\---

\


\## 二、Glow 是什么？

\[Glow]\(https://github.com/charmbracelet/glow) 是由 Charmbracelet 开发的一个 \*\*命令行 Markdown 渲染器\*\*，支持 GitHub 风格的渲染，具有如下特点：

\


\- ✅ 在终端中渲染 Markdown（支持标题、代码块、表格、高亮等） &#x20;

\- 🔎 可搜索与浏览当前目录及子目录中的 \`.md\` 文件 &#x20;

\- 💾 支持离线阅读与本地缓存 &#x20;

\- ⚙️ 支持主题切换（dark/light 等） &#x20;

\


使用示例：

\`\`\`bash

glow README.md

\`\`\`

\


若想全屏分页浏览：

\`\`\`bash

glow -p README.md

\`\`\`

\


\---

\


\## 三、Glamour 是什么？

\[Glamour]\(https://github.com/charmbracelet/glamour) 是 Glow 背后的 \*\*Markdown 渲染引擎\*\*，Glow 内部使用它来将 Markdown 转换为 ANSI 彩色输出。 &#x20;

你也可以单独使用 Glamour 来构建自己的 Markdown 终端工具。

\


\`\`\`bash

echo "# Hello Glamour" | glamour

\`\`\`

\


换句话说：

\> Glow 是带界面的工具，而 Glamour 是底层渲染引擎。

\


\---

\


\## 四、mdx 与 mdt 的终端 Markdown 系统

\


为了在终端中更方便地查看、搜索、编辑 Markdown 文件，我们结合了 Glow、fzf、ripgrep、vim 等工具，构建了 \*\*mdx/mdt 系统\*\*。

\


\### 1. mdx：Glow 版本（查看 + 搜索 + 编辑）

\


mdx 使用 Glow 作为渲染器，搜索并预览当前目录下的 Markdown 文件。

\


\`\`\`bash

mdx

\`\`\`

支持： &#x20;

\- 🔍 模糊搜索 Markdown 文件 &#x20;

\- 👀 Glow 渲染预览（右侧显示内容） &#x20;

\- ✏️ 选择文件后用 vim 打开编辑 &#x20;

\


安装脚本：

\`\`\`bash

brew install glow fzf ripgrep vim

\# curl -sSL https://github.com/VCBSstudio/Shell/blob/main/install\_mdx.sh | bash

curl -sSL https://raw.githubusercontent.com/VCBSstudio/Shell/main/install\_mdx.sh | bash

\


\`\`\`

\


但是：Glow 在新版中分页机制改动后（\`--pager=''\` 无效），导致部分终端中无法正常显示彩色高亮。

\


\---

\


\### 2. mdt：bat + glow 混合增强版

\


为了解决 Glow 分页与高亮问题，\`mdt\` 引入了 \`bat\`。 &#x20;

\`bat\` 是一个带语法高亮的 cat 替代工具，能在终端中美观地输出 Markdown 与代码。

\


\`mdt\` 的特性：

\- 🌈 彩色高亮（bat 提供更稳定的渲染效果） &#x20;

\- 🔍 支持 fzf 搜索与预览 &#x20;

\- ✏️ 多选并编辑 &#x20;

\- ⚙️ 支持 Glow 主题切换（备用） &#x20;

\


示例命令：

\`\`\`bash

mdt

\`\`\`

\


安装脚本会创建一个 \`$HOME/.local/bin/mdt\` 命令：

\`\`\`bash

brew install glow fzf ripgrep bat vim

\# curl -sSL https://github.com/VCBSstudio/Shell/blob/main/install\_mdt.sh | bash

curl -sSL https://raw.githubusercontent.com/VCBSstudio/Shell/main/install\_mdt.sh | bash

\


\`\`\`

\


\---

\


\## 五、Glow 与 Glamour 的关系

\


\| 工具 | 作用 | 是否渲染 Markdown | 是否有交互界面 |

\|------|------|------------------|----------------|

\| \*\*Glamour\*\* | Markdown → ANSI 彩色文本的渲染引擎 | ✅ | ❌ |

\| \*\*Glow\*\* | Glamour 的封装 CLI 工具，用于终端预览 Markdown | ✅ | ✅ |

\


简单来说：

\> Glamour 是“引擎”，Glow 是“整车”。

\


\---

\


\## 六、总结

\


\| 工具 | 功能 | 优点 | 适用场景 |

\|------|------|------|----------|

\| \*\*Glow\*\* | 渲染 Markdown | 轻量、简洁、美观 | 个人阅读、项目文档 |

\| \*\*mdx\*\* | 搜索 + Glow 预览 + 编辑 | 快速浏览与编辑 | 小型项目文档管理 |

\| \*\*mdt\*\* | bat 渲染 + Glow 兼容 | 彩色稳定、功能完整 | 全终端 Markdown 工作流 |

\| \*\*Glamour\*\* | 渲染引擎 | 可定制性强 | 自定义 CLI 工具开发 |

\


\---

\


\### 💡 推荐组合

如果你追求极致终端体验：

\`\`\`bash

brew install glow fzf ripgrep bat vim

export GLOW\_STYLE=dark

mdt

\`\`\`

\


\---

\


\*\*结语\*\* &#x20;

通过 Glow + Glamour + fzf + bat，我们终于能在终端中拥有媲美 VSCode 的 Markdown 浏览体验。
