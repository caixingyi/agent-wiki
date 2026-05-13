# Agent Wiki

AI Agent 开发资源、面试题库与项目实战指南。

Agent Wiki 用 Hugo + Hextra 构建，内容聚焦 AI Agent 学习、求职准备和项目实践。站点地址：<https://agentwiki.top/>

## 内容板块

| 板块 | 内容 |
| --- | --- |
| 学习资源 | Agent 框架教程、RAG 最佳实践、Tool Use 指南等 |
| 面经 | AI Agent 相关岗位面试真题、系统设计题与参考答案，按大厂、中厂、小厂、央国企分类 |
| 项目实战 | Agent 项目案例、实战教程与架构经验分享 |
| 他山之石 | 学习路线、踩坑经验、转型故事 |
| 贡献者 | 部署时自动读取 GitHub contributors 并展示 |

## 本地开发

### 前置条件

- [Hugo Extended](https://gohugo.io/installation/) 0.161.1 或兼容版本
- [Go](https://go.dev/doc/install) 1.22+
- [Git](https://git-scm.com/)

### 运行

```bash
git clone https://github.com/caixingyi/agent-wiki.git
cd agent-wiki

hugo mod get -u
hugo server -D
```

本地预览默认地址通常是 <http://localhost:1313/>。

### 构建

```bash
hugo --gc --minify
```

## 新增内容

```bash
# 新增学习资源
hugo new resources/my-article.md

# 新增面经
hugo new interview/small-company/my-interview.md

# 新增项目实战
hugo new projects/my-project.md

# 新增学习路线或经验分享
hugo new learning-paths/my-roadmap.md
```

面经目录当前按公司类型组织：

- `content/interview/big-company/`
- `content/interview/mid-company/`
- `content/interview/small-company/`
- `content/interview/state-owned/`

## 自动化

### GitHub Pages 部署

项目使用 GitHub Actions 部署到 GitHub Pages。推送到 `main` 后会自动触发 `.github/workflows/deploy.yml`。

部署流程会：

1. 安装 Hugo Extended
2. 拉取 Hugo module
3. 通过 GitHub API 生成 `data/contributors.json`
4. 构建静态站点
5. 发布到 GitHub Pages

### 贡献者页面

`content/contributors/_index.md` 使用 `{{< contributors >}}` shortcode。部署时生成的 `data/contributors.json` 会被 Hugo 读取，并由 `layouts/shortcodes/contributors.html` 渲染为贡献者卡片。

本地没有生成该 JSON 时，页面会显示占位提示；线上部署会自动更新真实贡献者列表。

## 贡献

欢迎提交内容和修正：

1. Fork 本仓库
2. 创建分支：`git checkout -b feature/my-article`
3. 添加或修改 `content/` 下的 Markdown 文件
4. 提交 Pull Request

更详细的说明见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

MIT
