# Hugo 博客

个人技术博客，使用 Hugo + Stack 主题搭建。

## 本地开发

```bash
# 启动本地服务器
hugo server -D

# 构建
hugo --gc --minify
```

## 新建文章

```bash
hugo new content posts/my-new-post/index.zh-cn.md
hugo new content posts/my-new-post/index.en.md
```

## 部署

推送到 `main` 分支后，GitHub Actions 会自动构建并部署到 GitHub Pages。

## 配置评论系统

1. 前往 [giscus.app](https://giscus.app) 配置你的仓库
2. 在 `hugo.yaml` 中填写 `repo`、`repoID`、`categoryID`

## 项目结构

```
blog/
├── content/
│   ├── posts/          # 博客文章
│   └── page/           # 独立页面（关于、作品集等）
├── static/img/         # 静态图片
├── themes/             # Hugo 主题
├── hugo.yaml           # 站点配置
└── .github/workflows/  # 自动部署
```
