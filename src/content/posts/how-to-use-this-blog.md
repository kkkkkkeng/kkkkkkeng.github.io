---
title: "How to use this blog"
description: "一份留给自己的博客使用指南：启动预览、撰写文章、修改配置。"
pubDatetime: 2026-10-23T17:00:00+08:00
tags:
  - blogging
  - guide
featured: true
draft: false
---

这个博客基于 Astro 和 AstroPaper。
## 启动本地预览

第一次使用或依赖更新后，先安装依赖。需要 Node.js 24 或更新版本：

```bash
npm ci
```

平时写作只需要启动开发服务：

```bash
npm run dev
```

打开终端显示的地址，通常是 `http://localhost:4321/`。保存文章后，页面会自动更新。如果端口被占用，以终端实际显示的地址为准。在前台运行服务的终端中按 `Ctrl+C` 可以停止服务。

想检查最终生成的网站和搜索功能，先构建，再启动预览：

```bash
npm run build
npm run preview -- --port 4322
```

打开 `http://localhost:4322/`。这个地址展示的是最近一次构建结果，修改内容后需要重新运行 `npm run build`。

## 新建一篇文章

文章放在 `src/content/posts/`，使用 Markdown 文件即可。例如：

```text
src/content/posts/my-first-post.md
```

复制下面的内容，再替换成自己的标题、简介和正文：

````markdown
---
title: "我的第一篇文章"
description: "这篇文章的简短介绍。"
pubDatetime: 2026-10-23T17:00:00+08:00
tags:
  - notes
featured: false
draft: true
---

## 开始记录

这里是正文。

- 一个想法
- 一条笔记

这是一个[链接](https://github.com/kkkkkkeng)。

```python
print("Hello, world!")
```
````

文件顶部两条 `---` 之间的内容叫 frontmatter，用来描述文章信息。

| 字段          | 用途                                                      |
| ------------- | --------------------------------------------------------- |
| `title`       | 文章标题，可以使用中文。                                  |
| `description` | 简短摘要，会出现在文章列表等位置。                        |
| `pubDatetime` | 首次发布时间，包含日期、时间和时区。                      |
| `modDatetime` | 可选，文章最近一次修改的时间。                            |
| `tags`        | 标签列表，网站会自动生成对应的标签页面。                  |
| `featured`    | 设为 `true`，文章出现在首页 Featured 区域。               |
| `draft`       | 设为 `true`，文章不会出现在网站中；准备好后改成 `false`。 |

文件名可使用简短的英文单词，用连字符连接。这篇指南的文件名是 `how-to-use-this-blog.md`，对应地址为 `/posts/how-to-use-this-blog/`。

### 日期、草稿和定时文章

北京时间可以写成 `2026-10-23T17:00:00+08:00`。也可以使用 UTC，例如 `2026-10-23T09:00:00Z`，这两个值表示同一时刻。

草稿在开发预览中也会隐藏。需要在页面上检查时，可以暂时设为 `draft: false`，检查完再改回去。

开发模式会显示非草稿的未来文章。正式构建会根据发布时间筛选文章，当前配置允许提前 15 分钟显示。网站是静态生成的，时间到了以后还需要重新构建、部署，文章才会出现。

修改已发布文章时，可以加上：

```yaml
modDatetime: 2026-10-24T10:00:00+08:00
```

## 常用 Markdown 写法

````markdown
## 二级标题

### 三级标题

**加粗**、_斜体_、`行内代码`。

> 一段引用。

- 无序列表
- 第二项

1. 第一步
2. 第二步

[链接文字](https://example.com)

```javascript
console.log("Hello, world!");
```
````

文章标题已经由 `title` 自动显示，正文通常从 `##` 开始，不必再重复写一个一级标题。

## 数学公式

博客启用 KaTeX，可以在 Markdown 和 MDX 正文中使用 LaTeX 公式。公式在构建时生成。

行内公式使用一对美元符号：

```markdown
质能方程为 $E = mc^2$。
```

实际效果：质能方程为 $E = mc^2$。

独立公式使用两对美元符号，并单独占行：

```markdown
$$
\frac{\partial \mathcal{L}}{\partial \theta}
= \frac{1}{N}\sum_{i=1}^{N}\nabla_\theta \ell_i(\theta)
$$
```

实际效果：

$$
\frac{\partial \mathcal{L}}{\partial \theta}
= \frac{1}{N}\sum_{i=1}^{N}\nabla_\theta \ell_i(\theta)
$$

矩阵也可以直接书写：

```markdown
$$
A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}
$$
```

$$
A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}
$$

公式使用 KaTeX 自带的数学字体，普通正文仍使用原主题字体。KaTeX 支持常用 LaTeX 数学语法。普通文字中需要显示美元符号时，可以写成 `\$`。

## 添加图片

把图片放进 `public/images/`，例如：

```text
public/images/my-desk.jpg
```

在文章中引用：

```markdown
![我的桌面](/images/my-desk.jpg)
```

引用路径不包含 `public`。方括号里的文字是图片的替代说明，建议简短描述图片内容。图片文件名也建议使用英文和连字符。

## 修改网站信息

| 想修改的内容                        | 对应文件                     |
| ----------------------------------- | ---------------------------- |
| 网站名称、简介、作者、GitHub 和邮箱 | `astro-paper.config.ts`      |
| 首页的问候语和介绍                  | `src/pages/index.astro`      |
| About 页面                          | `src/content/pages/about.md` |
| 文章                                | `src/content/posts/`         |
| 浏览器标签页图标                    | `public/favicon.svg`         |
| 分享网站链接时使用的默认封面        | `public/social-card.png`     |


英文使用主题原有的 Google Sans Code。汉字由浏览器使用系统中的备用字体显示，因此不同设备上的中文外观可能略有不同。

## 搜索、标签和归档

文章的 `tags` 会自动出现在 Tags 页面，Archives 会按时间组织文章，无需手动维护列表。

搜索索引在 `npm run build` 时生成。新增或修改文章后，重新构建再测试搜索，才能看到最新结果。匹配效果以实际生成的索引为准。

## 发布前检查

写完后先运行：

```bash
npm run build
```

构建会检查类型、生成静态页面并更新搜索索引。成功后，用 `npm run preview` 检查以下内容：

- 标题、简介、日期是否正确。
- 准备公开的文章是否设为 `draft: false`。
- 图片、链接和代码块是否正常。
- 手机宽度下的排版是否舒适。
- 明暗模式和搜索是否可用。

## 之后如何发布到 GitHub Pages

仓库中已经准备了 `.github/workflows/deploy.yml`。首次上线这次改版时，需要把 GitHub 仓库 Settings → Pages 中的发布来源改为 **GitHub Actions**。

推送后，在 GitHub 仓库的 Actions 页面查看部署结果。部署成功后，访问：

<https://kkkkkkeng.github.io/>

本地保存文件只会更新本地内容。提交、推送并成功部署后，线上读者就能看到更新啦:D。
