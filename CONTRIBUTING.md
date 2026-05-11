# 贡献指南

感谢你对 Agent Wiki 的关注！我们欢迎任何形式的贡献。

## 贡献方式

### 方式一：直接在网站上编辑（最简单）

1. 在 [Agent Wiki](https://caixingyi.github.io/agent-wiki/) 上找到你想修改的页面
2. 点击右侧的「在 GitHub 上编辑此页 →」
3. GitHub 会自动帮你 Fork 并打开编辑器
4. 修改完成后点击「Propose changes」
5. 然后点击「Create pull request」提交

### 方式二：本地开发

1. Fork 本仓库（点击右上角 Fork 按钮）
2. 克隆你 Fork 的仓库：
   ```bash
   git clone https://github.com/你的用户名/agent-wiki.git
   cd agent-wiki
   ```
3. 创建新分支：
   ```bash
   git checkout -b feature/你的主题
   ```
4. 本地预览（需要安装 [Hugo](https://gohugo.io/installation/) 和 [Go](https://go.dev/dl/)）：
   ```bash
   hugo server
   ```
5. 在 `content/` 对应目录下添加或修改 `.md` 文件
6. 提交并推送：
   ```bash
   git add -A
   git commit -m "docs: 描述你的改动"
   git push origin feature/你的主题
   ```
7. 回到 GitHub 页面，点击「Compare & pull request」提交 PR

## 文章格式

每篇文章开头需要包含 front matter：

```markdown
---
title: 文章标题
type: docs
weight: 1
sidebar:
  open: false
---

正文内容...
```

## 目录结构

| 目录 | 内容 |
|------|------|
| `content/resources/` | 学习资源：框架教程、论文解读、最佳实践 |
| `content/interview/` | 面经：面试真题、系统设计题 |
| `content/projects/` | 项目实战：实战教程、开源项目 |
| `content/community/` | 社区：周报、活动、讨论 |

## 注意事项

- 文章使用 Markdown 格式
- 图片放在 `static/images/` 目录下
- 提交信息请使用中文描述改动内容
