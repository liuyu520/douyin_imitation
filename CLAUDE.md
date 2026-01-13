# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`douyin-vue` 是一个模仿抖音/TikTok的移动端短视频Web应用，使用 Vue 3 + Vite 5 + Pinia + TypeScript 构建。数据通过 `axios-mock-adapter` 拦截API请求并返回本地JSON数据，无需后端服务。

## Common Commands

```bash
# 开发
pnpm dev              # 启动开发服务器 (端口3000, 自动打开浏览器)
pnpm lint             # ESLint检查并修复
pnpm format           # Prettier格式化
pnpm type-check       # TypeScript类型检查

# 构建
pnpm build            # 生产构建
pnpm build-gp-pages   # GitHub Pages构建
pnpm build-gitee-pages # Gitee Pages构建

# 提交
pnpm commit           # 使用Commitizen规范提交

# Docker
make docker-build     # 构建Docker镜像
make docker-run       # 运行容器
```

## Architecture

### 目录结构

```
src/
├── api/           # API请求层 (user.ts, videos.ts)
├── components/    # 可复用组件 (slide/, dialog/, mobile-select/)
├── pages/         # 路由页面 (home/, login/, me/, message/, shop/)
├── router/        # 路由配置 (index.ts定义路由, routes.ts定义路由表)
├── store/         # Pinia状态管理 (pinia.ts - useBaseStore)
├── utils/         # 工具函数
│   ├── hooks/     # Vue组合式API hooks
│   ├── request.ts # Axios封装
│   ├── bus.ts     # 事件总线
│   └── slide.ts   # 滑动逻辑
├── mock/          # Mock数据配置
├── config/        # 环境配置
└── assets/        # 静态资源 (data/, img/, less/)
```

### 核心模式

**状态管理 (Pinia)**
- `useBaseStore`: 全局状态 - bodyHeight/Width, userinfo, users, friends, maskDialog, excludeNames(路由缓存排除)

**Mock系统**
- 使用 `axios-mock-adapter` + `MockJS` 拦截所有API
- 数据文件位于 `public/data/` 和 `src/assets/data/`
- API端点: `/video/recommended`, `/video/comments`, `/user/panel`, `/user/friends`, `/shop/recommended`

**路由**
- 根据 `IS_SUB_DOMAIN` 配置选择Hash或History模式
- 使用 `keep-alive` + `excludeNames` 实现选择性页面缓存
- 路由深度决定进入/返回动画方向

**HTTP请求**
- 封装在 `src/utils/request.ts`
- 统一返回格式: `{ success, data, code }`

## Development Notes

- **移动端预览**: 必须使用浏览器手机模式 (F12 + Ctrl+Shift+M)
- **视口宽度**: 限制在500px，使用rem和动态vh自适应
- **路径别名**: `@/` 指向 `./src/`
- **环境配置**: 位于 `env/` 目录 (.env, .env.prod, .env.gp_pages等)

## Code Style

- Prettier配置: 单引号, 无分号, 2空格缩进, 100字符行宽
- 使用 `pnpm commit` 进行约定式提交
- lint-staged 自动格式化提交的代码
