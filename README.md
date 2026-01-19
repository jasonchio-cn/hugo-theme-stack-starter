# hugo-theme-stack-starter

> ⚙️ Hugo 站点配置与构建仓库 - 拉取内容、构建 Hugo、推送发布产物

## 简介

这个仓库负责 Hugo 站点的配置/主题自定义，以及 GitHub Actions 构建流水线。

- 内容来源：`jasonchio-cn/ObsidianVault`
- 构建工具：Hugo (extended) + Hugo Modules
- 发布目标：将构建产物推送到 `jasonchio-cn/jasonchio-cn.github.io` 的 `main`

## 三仓库架构

```
┌─────────────────────────────────────────────────────────────┐
│ 1) ObsidianVault                                              │
│    - 写作：Markdown 文章                                      │
│    - 资源：assets/                                            │
└──────────────────────────┬──────────────────────────────────┘
                           │  repository_dispatch: content-update
                           ↓
┌─────────────────────────────────────────────────────────────┐
│ 2) hugo-theme-stack-starter (本仓库)                           │
│    - Hugo 配置 + 主题自定义                                   │
│    - 构建 Hugo 并产出 public/                                 │
└──────────────────────────┬──────────────────────────────────┘
                           │  push (build output)
                           ↓
┌─────────────────────────────────────────────────────────────┐
│ 3) jasonchio-cn.github.io                                     │
│    - GitHub Pages 发布仓库（最终静态站点）                     │
└─────────────────────────────────────────────────────────────┘
```

## 这个仓库负责什么

- Hugo 配置：`config/`
- 主题与自定义资源：`assets/`、`static/`、Hugo Modules
- CI/CD：`.github/workflows/deploy.yml`（构建并推送到发布仓库）

## 自动化机制

### 触发

- `push` 到 `master`
- `repository_dispatch`（`content-update`，通常由 ObsidianVault 触发）

### 构建与发布

- 拉取本仓库（配置）
- 拉取 `ObsidianVault`（内容源）到 `content-source/`
- 合并内容：
  - `content-source/*.md` -> `content/post/`
  - `content-source/assets/` -> `content/assets/`
- Hugo 构建：`hugo --minify --gc --configDir config`
- 推送构建产物：`public/` -> `jasonchio-cn/jasonchio-cn.github.io` 的 `main`

## 必要的 Secrets

在本仓库 `Settings -> Secrets and variables -> Actions` 配置：

- `PAT_TOKEN`
  - 需要能读取 `ObsidianVault`，并能写入 `jasonchio-cn.github.io`
  - 建议最简单用 classic PAT 的 `repo` 权限（或细粒度 token 给两个仓库对应权限）

## 本地开发

```bash
git clone https://github.com/jasonchio-cn/hugo-theme-stack-starter.git
cd hugo-theme-stack-starter
hugo server --configDir config
```

如果需要本地带内容预览：

```bash
git clone https://github.com/jasonchio-cn/ObsidianVault.git ../ObsidianVault
mkdir -p content/post content/assets
cp -v ../ObsidianVault/*.md content/post/ || true
cp -rv ../ObsidianVault/assets content/assets || true
hugo server --configDir config
```

## 相关仓库

| 仓库 | 用途 | 链接 |
| --- | --- | --- |
| ObsidianVault | 内容管理 | https://github.com/jasonchio-cn/ObsidianVault |
| hugo-theme-stack-starter | Hugo 配置/构建（本仓库） | https://github.com/jasonchio-cn/hugo-theme-stack-starter |
| jasonchio-cn.github.io | 发布仓库 | https://github.com/jasonchio-cn/jasonchio-cn.github.io |

## 快速链接

- 博客：https://jasonchio-cn.github.io
- Actions（构建仓库）：https://github.com/jasonchio-cn/hugo-theme-stack-starter/actions

## 更新日志

- 2026-01-19: 统一三仓库 README 风格，README 同步当前部署方式
