# 🤖 Agent Wiki — AI Agent 开发资源与面试社区

> AI Agent 开发的一站式资源平台：学习资源、面试题库、项目实战、社区交流

## 📖 板块介绍

| 板块 | 内容 |
|------|------|
| 📚 **学习资源** | Agent 框架教程、论文解读、最佳实践 |
| 💼 **面试题库** | Agent 相关岗位面试真题与参考答案 |
| 🏗️ **项目实战** | 开源项目推荐、实战教程 |
| 👥 **社区** | 行业周报、技术讨论、活动信息 |

## 🚀 本地开发

### 前置条件
- [Hugo Extended](https://gohugo.io/installation/) (v0.120+)
- [Git](https://git-scm.com/)

### 运行

```bash
# 克隆仓库（含主题子模块）
git clone --recurse-submodules https://github.com/YOUR_USERNAME/agent-wiki.git
cd agent-wiki

# 本地预览
hugo server -D

# 构建
hugo --minify
```

### 新增内容

```bash
# 新增资源文章
hugo new resources/my-article.md

# 新增面试题
hugo new interview/my-question.md

# 新增项目实战
hugo new projects/my-project.md

# 新增社区动态
hugo new community/my-post.md
```

## 🌐 部署

本项目使用 **GitHub Actions** 自动部署到 **GitHub Pages**：

1. 在 GitHub 创建仓库 `agent-wiki`
2. 进入仓库 **Settings → Pages → Source**，选择 **GitHub Actions**
3. 修改 `hugo.yaml` 中的 `baseURL` 为你的 GitHub Pages 地址
4. 推送代码到 `main` 分支，自动触发部署

## 🤝 贡献

欢迎社区贡献！你可以：

1. **Fork** 本仓库
2. 创建你的分支 (`git checkout -b feature/my-article`)
3. 提交更改 (`git commit -m 'Add: 新文章'`)
4. 推送分支 (`git push origin feature/my-article`)
5. 创建 **Pull Request**

## 📄 License

[MIT](LICENSE)
