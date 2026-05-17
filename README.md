<div align="center">

# GuadaClaw 🦾

> 智能 AI 对话系统，支持 ReAct Agent、多模型适配、RAG 知识库检索、MCP 工具调用与 Skills 技能框架，深度集成 OpenClaw 能力。

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/andoaidlaksldk/GuadaClaw/build.yml?style=flat-square)
![GitHub](https://img.shields.io/github/license/andoaidlaksldk/GuadaClaw?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/andoaidlaksldk/GuadaClaw?style=flat-square)
![GitHub repo size](https://img.shields.io/github/repo-size/andoaidlaksldk/GuadaClaw?style=flat-square)

[![NestJS](https://img.shields.io/badge/NestJS-11.x-red.svg?style=for-the-badge&logo=nestjs)](https://nestjs.com)
[![Vue](https://img.shields.io/badge/Vue-3.x-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.x-blue.svg?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org)
[![Prisma](https://img.shields.io/badge/Prisma-7.x-2D3748?style=for-the-badge&logo=prisma&logoColor=white)](https://www.prisma.io)
[![Electron](https://img.shields.io/badge/Electron-31.x-47848F?style=for-the-badge&logo=electron&logoColor=white)](https://www.electronjs.org)

</div>

---

## 📋 目录

- [系统概览](#系统概览)
- [核心特性](#核心特性)
- [技术栈](#技术栈)
- [快速开始](#快速开始)
- [项目结构](#项目结构)
- [许可证](#许可证)

---

## 🌟 系统概览

GuadaClaw 是一个功能完备的 AI 对话和工作辅助平台，集成了**浏览器自动化**、**RAG 知识库**、**MCP 协议**和**Skills 技能框架**，深度集成 OpenClaw 能力。

### 🎯 架构特点

| 特性 | 说明 |
|------|------|
| **双入口设计** | REST + SSE API 和 Bot Gateway 对等入口 |
| **Agent 中心化** | 所有能力经由 Agent 循环统一调度 |
| **插拔式扩展** | 工具、技能、模型适配器支持热插拔 |
| **长上下文管理** | 两级压缩策略，Token 成本可控 |
| **浏览器自动化** | Electron 内嵌浏览器引擎，突破 API 边界 |

### 🖼️ 产品截图

![产品截图1](./images/1.png)

---

## ✨ 核心特性

### 🤖 Agent 对话引擎

实现 **ReAct (Reasoning + Acting)** 模式的多轮自治循环引擎：

- **会话锁**：同一会话同时仅处理一个请求
- **流式传输**：SSE 异步实时渲染
- **中断处理**：客户端断开自动中止，节省 Token
- **思考追踪**：记录推理耗时，存储于消息元数据

### 📚 知识库 (RAG)

完整的检索增强生成流程：

- **自助多轮搜索**：Agent 自主决定搜索策略
- **混合检索**：语义搜索 + 关键词搜索加权融合
- **支持 40+ 文件格式**：PDF/DOCX/TXT 等自动解析

### 🛠️ Skills 技能框架

基于 **Anthropic Skills 协议** 设计：

- **热插拔**：文件系统存储，支持动态加载
- **渐进式披露**：L1/L2 分级指令注入

### 🔗 Bot 网关

多平台即时通讯适配：

- **统一接口**：策略模式，新平台接入只需实现接口
- **自动重连**：WebSocket 断连后指数退避重试
- **消息合并**：1.5 秒窗口内多条消息合并处理

---

## 🛠️ 技术栈

### 后端
| 技术 | 版本 | 用途 |
|------|------|------|
| NestJS | 11.x | 服务端框架 |
| TypeScript | 6.x | 类型安全 |
| Prisma | 7.x | ORM |
| SQLite | - | 数据库 |
| sqlite-vec | - | 向量存储 |

### 前端
| 技术 | 版本 | 用途 |
|------|------|------|
| Vue 3 | - | UI 框架 |
| Vite | 6.x | 构建工具 |
| Element Plus | - | UI 组件库 |
| Pinia | - | 状态管理 |

### 桌面
| 技术 | 版本 | 用途 |
|------|------|------|
| Electron | 31.x | 桌面应用框架 |

---

## 🚀 快速开始

### 环境要求

- Node.js ≥ 18.x（推荐 20.x LTS）
- npm ≥ 9.x

### 启动后端

```bash
cd backend-ts
npm install              # 安装依赖
npm run db:seed:force    # 初始化种子数据（admin / admin）
npm run start:dev        # 开发模式 → http://localhost:3000
```

### 启动前端

```bash
cd frontend
npm install
npm run dev              # 开发模式 → http://localhost:5173
```

### 部署文档

- [生产环境部署](docs/PRODUCTION_DEPLOYMENT.md)
- [Electron 部署](docs/ELECTRON_DEPLOYMENT.md)
- [故障排查](docs/TROUBLESHOOTING.md)

---

## 📁 项目结构

```
GuadaClaw/
├── backend-ts/          # NestJS 后端
│   ├── prisma/          # 数据库 Schema
│   ├── src/
│   │   ├── common/      # 基础设施
│   │   └── modules/     # 业务模块
│   │       ├── chat/    # 核心对话
│   │       ├── tools/   # 工具调用
│   │       ├── skills/  # 技能框架
│   │       └── knowledge-base/  # RAG 知识库
│   └── skills/          # Skills 目录
├── frontend/            # Vue 3 前端
│   └── src/
│       ├── components/  # UI 组件
│       ├── composables/ # 组合式函数
│       └── stores/      # Pinia 状态管理
├── build-resources/     # 构建资源
├── docs/                # 文档
└── scripts/             # 脚本工具
```

---

## 📄 许可证

本项目基于 [MIT License](LICENSE) 开源。

---

<div align="center">

**GuadaClaw** - 打造你的个人智能助理 🦾

</div>