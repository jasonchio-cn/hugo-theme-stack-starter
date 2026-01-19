# JasonChio 的 Hugo 博客配置仓库

这是基于 [Hugo Theme Stack Starter Template](https://github.com/CaiJimmy/hugo-theme-stack-starter) 修改的个人博客配置仓库。

## 📝 工作流

```
ObsidianVault (内容来源)
      ↓ (CI/CD)
hugo-theme-stack-starter (配置仓库)
      ↓ (部署)
jasonchio-cn.github.io (GitHub Pages)
```

## 🚀 功能特性

- ✅ **Hugo Theme Stack v3**：现代化的 Hugo 博客主题
- ✅ **Go Modules 主题管理**：自动化的主题更新
- ✅ **GitHub Actions CI/CD**：自动构建和部署
- ✅ **内容分离**：来自 ObsidianVault 的 Markdown 内容
- ✅ **自动部署**：推送到 master 分支自动触发部署

---

## 📖 快速开始

### 1. 仓库说明

本仓库包含：
- `config/_default/`：Hugo 配置文件
- `.github/workflows/`：自动化工作流（部署 + 主题更新）
- `assets/`：自定义资源（图标、样式、脚本）
- `static/`：静态资源文件

### 2. 配置 Secrets

在仓库设置中添加以下 Secrets：

| Secret 名称 | 说明 | 示例 |
|------------|------|------|
| `PAT_TOKEN` | GitHub Personal Access Token | 用于访问 ObsidianVault 私有仓库 |

**获取 PAT Token**：
1. 访问 [GitHub Settings → Developer settings → Personal access tokens](https://github.com/settings/tokens)
2. 创建新 token，勾选 `repo` 权限
3. 在 [本仓库 Settings → Secrets and variables → Actions](https://github.com/jasonchio-cn/hugo-theme-stack-starter/settings/secrets/actions) 中添加

### 3. 配置 GitHub Pages

1. 访问 [Settings → Pages](https://github.com/jasonchio-cn/hugo-theme-stack-starter/settings/pages)
2. 设置：
   - **Source**: Deploy from a branch
   - **Branch**: `gh-pages` / `root`

---

## 🛠️ 配置文件说明

### 网站基础配置 (`config/_default/config.toml`)
- `baseurl`: 网站地址
- `languageCode`: 语言代码
- `title`: 网站标题
- `theme`: 主题（使用 Go Modules）

### 主题参数 (`config/_default/params.toml`)
- 侧边栏、头像、社交媒体
- 评论系统（Twikoo）
- 小部件配置
- 颜色主题

### 菜单配置 (`config/_default/menu.toml`)
- 主导航菜单
- 社交媒体链接

---

## 🔄 工作流说明

### 自动部署 (`.github/workflows/deploy.yml`)

触发条件：
- 推送到 `master` 分支
- 创建 Pull Request

流程：
1. Checkout 配置仓库
2. Checkout 内容仓库（ObsidianVault）
3. 合并内容到 `content/` 目录
4. 安装 Hugo
5. 下载主题依赖
6. 构建网站（`hugo --minify --gc`）
7. 部署到 `gh-pages` 分支

### 自动主题更新 (`.github/workflows/update-theme.yml`)

触发条件：
- 每天 UTC 00:00
- 手动触发（在 Actions 页面点击 "Run workflow"）

流程：
1. 使用 `hugo mod get -u` 更新主题
2. 使用 `hugo mod tidy` 清理依赖
3. 提交变更

---

## 🧪 本地开发

### 环境要求
- Git
- Go 1.17+
- Hugo Extended (最新版本)

### 克隆仓库
```bash
git clone https://github.com/jasonchio-cn/hugo-theme-stack-starter.git
cd hugo-theme-stack-starter
```

### 运行开发服务器
```bash
hugo server
```

访问 `http://localhost:1313` 查看效果

### 本地预览来自 ObsidianVault 的内容
```bash
# 克隆 ObsidianVault 仓库到本地
git clone https://github.com/jasonchio-cn/ObsidianVault.git ../ObsidianVault

# 复制 content 目录
cp -r ../ObsidianVault/content .

# 启动开发服务器
hugo server
```

---

## 📝 内容管理

### 内容来源

博客内容来自 [ObsidianVault](https://github.com/jasonchio-cn/ObsidianVault) 仓库的 `content/` 目录。

### 内容结构

```
content/
├── post/              # 博客文章
│   ├── hello-world/
│   └── ...
├── page/              # 独立页面
│   └── about/
└── categories/        # 分类页面
```

### 文章 Front Matter 示例

```markdown
---
title: "文章标题"
date: 2025-01-19T00:00:00+08:00
lastmod: 2025-01-19T00:00:00+08:00
draft: false
authors:
  - JasonChio
categories:
  - 技术
tags:
  - Hugo
  - 博客
description: "文章描述（可选）"
featuredImage: "/images/featured.jpg"  # 可选
---
```

---

## 🔧 手动更新主题

```bash
hugo mod get -u github.com/CaiJimmy/hugo-theme-stack/v4
hugo mod tidy
```

---

## 📊 网站统计

- [Google Analytics](https://analytics.google.com/) ID: `G-YQ9F51F77Q`

---

## 🌐 相关链接

- **博客**: https://blog.961110.xyz:10010
- **配置仓库**: https://github.com/jasonchio-cn/hugo-theme-stack-starter
- **内容仓库**: https://github.com/jasonchio-cn/ObsidianVault
- **部署仓库**: https://github.com/jasonchio-cn/jasonchio-cn.github.io
- **主题**: https://github.com/CaiJimmy/hugo-theme-stack

---

## 📄 许可证

本项目基于 [MIT License](LICENSE) 开源。

主题版权归属 [CaiJimmy](https://github.com/CaiJimmy)。