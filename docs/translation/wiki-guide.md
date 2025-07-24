---
tags:
  - translation
  - osu!
  - osu!wiki
  - contribution
  - guide
  - WIP
comments: true
---

# osu!wiki 翻译指南

这篇文章作为 [osu!wiki 贡献指南](https://osu.ppy.sh/wiki/zh/osu%21_wiki/Contribution_guide)的补充与延伸，旨在向有志于参与 osu!wiki 中文翻译的人简单介绍一下贡献流程，以及在此过程中，一些可以用到的工具与资源。与此同时，提出一些发展性的建议，让 osu!wiki 的原文及翻译更能被理解，简明易懂，受欢迎。

## 1. 寻找目标

绝大多数贡献者（包括我）通常是在官网阅读 wiki 时遇到翻译过期或缺少翻译的提示时，突然就萌生出了想要自己翻译对应文章的冲动... 这确实是很正常的现象。

概括起来，osu!wiki 的翻译工作归为以下两类：

- 新翻译：从头开始翻译一篇文章
- 修订翻译：依照原文更新文章翻译，或者改善现有翻译

不过，如果你想要了解整个 wiki 的翻译情况，[cl8n 的小网站](https://osu.wiki/status/zh "osu!wiki 状态跟踪（简体中文翻译）")应该能派上用场。具体用法[请见下文](#tracker-usage)。

## 2. 翻译与自查

决定好要做的事情后，就可以开始翻译了。

## 附录

这一小节收纳了一些常用工具与资源，部分内容基于个人经验给出。

### 本地开发环境 {#dev-env}

如果你打算在本地编辑 osu!wiki 的内容，需要以下工具：

- 文本编辑器（支持 Markdown 与 EditorConfig 者较好）
- Git：用于版本控制、拉取与提交更改

笔者常用的是 VS Code / Code OSS 与 Kate。后者自带 Markdown 的格式支持，前者可以通过安装插件来实现；

- markdownlint
- EditorConfig for VS Code

### osu!wiki 规范 {#official-criteria}

目前 osu!wiki 中存在已经很完备的规范性文章，同时也有为贡献者准备的贡献指南。

- [贡献指南](https://osu.ppy.sh/wiki/zh/osu!_wiki/Contribution_guide)：集中于讲述一篇文章（翻译）从编辑到呈现的全过程，建议新人先去通读
- [文章风格规范](https://osu.ppy.sh/wiki/zh/Article_styling_criteria)：分为[排版](https://osu.ppy.sh/wiki/zh/Article_styling_criteria/Formatting)与[写作](https://osu.ppy.sh/wiki/zh/Article_styling_criteria/Writing)两部分，是 osu! wiki 的强制执行样式标准

如果在实际翻译时依然不熟悉具体的规则，可以参照英文原文的排版进行翻译。

### 术语表与参考 {#terms-reference}

[osu!ATRI](https://github.com/osu-atri) 中译组织在其网站上维护着一份简单的分类术语表，可以在 [GitHub Pages](https://osu-atri.github.io/osu-dictionary) 访问。

### 使用 wiki 状态跟踪网站 {#tracker-usage}

为了让 wiki 翻译者之间能协调翻译工作，[clayton (cl8n)](https://github.com/cl8n) 写了这样一个跟踪网站，通过拉取 osu-wiki 仓库源代码并进行解析，获取各个文章的翻译与更新状态。项目源码可在 [GitHub](https://github.com/cl8n/osu-wiki-status) 上查看。

打开主页面后显示的信息如下：

![跟踪网站主页面](img/tracker-main.png "跟踪网站主页面")

页面右侧显示 osu!wiki 支持的所有语言，红色数字为对应语言需要处理的文章数目，点击可切换到不同语言的跟踪页面。

页面左侧（主体）会列出所有需要处理的文章与分类，这些状态往往由 wiki 维护者作为标签添加到源文件，跟踪工具解析后显示：

- Outdated translations：翻译过期，需要依照原文更新。
- Missing articles / stubs：文章缺少翻译。
- Needs cleanup：因内容或结构上的问题而需要重写/重译。
- No native review：没有其他人审阅，通常是因为 PR 长时间没人审阅。

除此之外，如果英文原文有特殊状态（如过时），则会另立分类列出。点击文件名会跳转到 GitHub 仓库的对应文件页面。

对于过期翻译，页面会列出它们的过期时间（被标记为过期的时间），同时给出差异 (`EN diff`)。

![文件差异预览](img/tracker-diff-view.png "文件差异预览")

差异预览页面会简单显示出最新版本文件相对于前一版本的更改，在自检或者为他人审阅时都能使用，可以有效找出漏译错译的内容。当然如果有条件，可以使用其他更加强大或顺手的历史差异比较工具...
