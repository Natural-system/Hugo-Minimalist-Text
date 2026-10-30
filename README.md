# Hugo Minimalist Text 个人极简纯文字网站
这个开源项目是基于 hugo 构建，为了快速地发布文章，提升阅读体验，长久免费储存托管在github而设计为纯文字博客，最大降低占用容量，快速响应
---

🌟 核心技术特性一览
🎨 多色主题自由切换 —— 基于 CSS 变量体系的无闪技术方案

技术实现：通过 localStorage + document.documentElement.setAttribute('data-theme', targetTheme) 实现零闪动切换。

所有颜色变量（背景色、文字色、边框色、强调色）集中托管于 :root 与 html[data-theme] 伪类，切换过程无需重绘整个 DOM，仅改变 CSS 变量值。

主题切换器的圆形按钮采用高亮当前模式，状态持久化保存在浏览器本地。

该主题体系与页面上的代码块配色联动，暗黑模式下的代码块背景自动适配为深色，全文保持视觉一致性。

🧠 双轨内容架构 —— posts 与 logs 分离设计

本项目的核心设计理念是“正式文章”与“碎片随感”分轨管理：

正式文章 (content/posts/)：收录于独立 Markdown 文件，支持分类、标签及自动生成的侧边栏 TOC 目录。

日常日志 (content/logs/)：按年份独立成页（如 2025.md, 2026.md），采用时间线分组 + 滚动触底懒加载（IntersectionObserver API）架构，由专属模板 layouts/logs/single.html 精准渲染。

技术亮点：

日志懒加载机制：首次仅渲染首批日志，滚动至底部触发点后动态分批加载剩余条目，显著降低首屏加载压力，适合日志体量较大的长期写作。

时间线侧栏导航：自动解析日志结构，点击任意日期可平滑滚动（scrollIntoView）并附带高亮动画。

📊 阅读进度条 + 文章目录联动 —— 极简交互的细节注入

进度条：固定于页面顶部的进度指示器通过监听滚动事件实时计算已读百分比，宽度随滚动动态更新。

文章目录 (TOC)：

在文章页中利用 JavaScript 扫描正文下的所有 h2 与 h3 元素，自动生成嵌套无序列表。

若标题未手动设置 id，脚本会以 toc-heading-{index} 格式自动补全，确保锚点跳转正常。

目录悬浮于侧边栏，随页面滚动保持固定 (position: sticky)，并具备悬停微交互效果。

🔍 全站全文搜索 —— 基于 Hugo 构建时的数据预埋

技术思路：利用 Hugo 构建阶段的强大模板能力，将所有文章的标题、URL、发布日期等序列化为全局数据，通过内联脚本实现高性能检索。

匹配逻辑支持实时响应，无需依赖任何第三方搜索引擎，完全脱机可用，且响应迅速。

🧩 代码块一键复制 —— 提升技术写作的阅读体验

每个 <pre> 代码块在页面加载完成后，由 JavaScript 动态注入复制按钮。

使用 navigator.clipboard.writeText API 实现复制，并提供“已复制!”的状态反馈，平时低调隐藏以避免干扰阅读视线。

📆 智能分页与独立页面拓展

首页与分类页：采用纯前端 JS 驱动分页，并附带页码跳转输入框，支持直接输入数字快速跳转。

丰富的独立页面：通过 content/ 下的独立 Markdown 文件（如 about.md 关于页、community.md 问答交流页、archive.md 年份归档等），让整站功能更加立体。

🗂️ 项目目录结构

Plaintext


.
├── .github/workflows/
│     └─ hugo.yml             # GitHub Actions 自动化部署配置
├── content/                  # 内容源目录
│   ├── about.md              # 关于页面
│   ├── archive.md            # 年份归档页
│   ├── categories.md         # 分类归档页
│   ├── community.md          # 问答交流页（支持独立评论体系）
│   ├── log.md                # 随想日志引导页
│   ├── _index.md             # 首页内容源
│   ├── logs/                 # 碎片日志（按年度分文件管理）
│   │     ├── 2025.md
│   │     └── 2026.md
│   └── posts/                # 正式文章目录
│         ├── 2012-12-10-疯狂的两天.md
│         └── 2012-12-13-自然生活，假期的放松，徒步旅行20公里.md
├── layouts/                  # 页面布局模板 (Hugo 核心)
│   ├── archive.html          # 归档页布局
│   ├── categories.html       # 分类页布局
│   ├── index.html            # 首页布局（含 JS 分页）
│   ├── log.html              # 日志入口布局
│   ├── categories/
│   │     └── list.html       # 分类详情列表模板
│   ├── logs/
│   │     └── single.html     # 日志单页懒加载与时间线模板
│   └── _default/
│         ├── baseof.html     # 全局基础骨架
│         └── single.html     # 文章单页模板（TOC + 评论）
├── hugo.toml                 # Hugo 核心配置文件
├── patch_permalink.py        # 自定义路由/链接修补脚本
└── README.md                 # 本说明文件
🚀 快速开始 (本地开发)

确保已安装 Hugo 客户端：

Bash


git clone https://github.com/Natural-system/Hugo-Minimalist-Text
cd self-transcendence
hugo server
# 打开浏览器访问 http://localhost:1313
📄 开源协议

本项目采用 MIT License，欢迎 Fork、二次开发与使用。

如果你喜欢这个全新的 Hugo 博客体系，请点亮 Star ⭐ 支持一下！




