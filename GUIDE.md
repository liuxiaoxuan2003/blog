# 博客使用指南

## 博客地址

- 网站：https://liuxiaoxuan2003.github.io/blog/
- GitHub 仓库：https://github.com/liuxiaoxuan2003/blog
- 自动部署：每次 `git push` 到 main 分支，GitHub Actions 会自动构建并更新网站

## 日常更新博客流程

```bash
cd /Users/liuxiaoxuan/code/sufe/blog

# 写新文章（中文）
hugo new content posts/my-new-post/index.zh-cn.md

# 写新文章（英文）
hugo new content posts/my-new-post/index.en.md

# 本地预览（含草稿）
hugo server -D

# 推送上线
git add -A && git commit -m "新文章" && git push
```

## 文章模板

每篇文章的头部 (front matter) 格式：

```yaml
---
title: "文章标题"
slug: "url-slug"
description: "文章描述"
date: 2026-05-14
categories:
  - 推荐系统
tags:
  - RecSys
  - 深度学习
---

正文内容（Markdown 格式）...
```

## 项目结构

```
blog/
├── content/
│   ├── posts/              # 博客文章（每篇一个文件夹）
│   │   ├── recsys-intro/
│   │   │   ├── index.zh-cn.md
│   │   │   └── index.en.md
│   │   └── ...
│   └── page/               # 独立页面
│       ├── about/          # 关于我
│       ├── portfolio/      # 作品集
│       ├── archives/       # 归档
│       └── search/         # 搜索
├── static/img/             # 静态图片（头像等）
├── themes/hugo-theme-stack/ # 主题（git submodule）
├── hugo.yaml               # 站点配置
├── .github/workflows/      # GitHub Actions 自动部署
└── README.md
```

## 常用操作

### 添加文章封面图

把图片放到文章文件夹内，然后在 front matter 中引用：

```yaml
---
title: "文章标题"
image: cover.jpg
---
```

### 修改个人信息

- 关于页面：`content/page/about/index.zh-cn.md`
- 作品集：`content/page/portfolio/index.zh-cn.md`
- 站点配置（标题、侧边栏等）：`hugo.yaml`

### 配置评论系统

1. 前往 https://giscus.app 配置仓库
2. 编辑 `hugo.yaml`，填写以下字段：

```yaml
params:
  comments:
    giscus:
      repo: "liuxiaoxuan2003/blog"
      repoID: "你的 repoID"
      category: "Announcements"
      categoryID: "你的 categoryID"
```

### 更换头像

替换 `static/img/avatar.jpg` 文件即可。

### 数学公式

文章中直接使用 LaTeX 语法：

```markdown
行内公式：$E = mc^2$

独立公式：
$$\nabla_\theta J(\theta) = \mathbb{E}\left[\sum_t \nabla_\theta \log \pi_\theta(a_t|s_t) \cdot G_t\right]$$
```

## 技术栈

- **框架**：Hugo v0.161.1
- **主题**：Stack (hugo-theme-stack)
- **部署**：GitHub Pages + GitHub Actions
- **功能**：中英双语、暗色模式、搜索、评论(giscus)、LaTeX 公式
