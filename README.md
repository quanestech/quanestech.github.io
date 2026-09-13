# Hexo Blog

这个仓库用于发布到 `https://quanestech.github.io/` 的 Hexo 静态博客，支持两种内容来源：

- 直接提交到 `source/_posts/*.md` 的 Markdown 文章
- GitHub Issues 中带有 `blog` 或 `post` 标签的内容

GitHub Actions 会在推送到 `main`、更新带标签的 Issue、或手动运行时构建站点并发布到 GitHub Pages。

## 本地开发

```bash
npm install
npm run server
```

本地预览地址默认是：

```text
http://localhost:4000
```

新建文章：

```bash
npm run new -- "文章标题"
```

生成静态文件：

```bash
npm run build
```

生成结果在 `public/`，不会提交到 Git。

## 用 Markdown 写文章

把文章放到：

```text
source/_posts/
```

每篇文章建议包含 Front Matter：

```markdown
---
title: 文章标题
date: 2026-09-13 12:00:00
tags:
  - notes
categories:
  - blog
---

文章正文。
```

## 用 Issue 写文章

在 GitHub 仓库中创建 Issue，并添加以下任一标签：

- `blog`
- `post`

Issue 正文会被同步成 Hexo Markdown 文章参与构建。可选地在 Issue 正文顶部写 Front Matter：

```markdown
---
title: 自定义标题
date: 2026-09-13 12:00:00
tags:
  - github
---

正文内容。
```

如果没有写 Front Matter，脚本会使用 Issue 标题、创建时间、标签和链接自动生成。

## GitHub Pages 设置

1. 打开 GitHub 仓库的 `Settings > Pages`。
2. 在 `Build and deployment` 中选择 `GitHub Actions`。
3. 推送到 `main` 后，Actions 会自动发布。

如果使用独立部署密钥，先把本机公钥添加到仓库。当前建议使用为这个仓库单独生成的公钥：

```bash
pbcopy < ~/.ssh/id_ed25519_quanestech.pub
```

复制到 GitHub 仓库 `Settings > Deploy keys` 中添加。如果要从本机 push，需要勾选写权限。
