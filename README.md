# kkkkkkeng's Blog

基于 [AstroPaper](https://github.com/satnaing/astro-paper) 的个人博客。

网站：https://kkkkkkeng.github.io/

需要 Node.js 24 或更新版本。使用 `npm ci` 安装依赖，`npm run dev` 本地开发，`npm run build` 检查类型、构建页面并生成搜索索引，`npm run preview` 预览构建结果。

- 文章：`src/content/posts/`，支持 Markdown / MDX，目前为空。
- 关于：`src/content/pages/about.md`。
- 标题、简介、社交链接：`astro-paper.config.ts`。
- 首页：`src/pages/index.astro`。

文章格式：

```md
---
title: "我的第一篇文章"
description: "文章简介"
pubDatetime: 2026-10-23T08:00:00Z
tags: [notes]
draft: false
---

在这里开始写作。
```

推送到 `main` 后，GitHub Actions 会自动构建并发布到 GitHub Pages。主题的 MIT 许可保留在 `LICENSE`。
