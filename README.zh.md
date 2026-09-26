# CeXia (策匣)

[English](README.md)

![CeXia Logo](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/resources/logo_256.png)

智能 AI 任务协同调度平台 — 由 9 个专业化 AI Agent 7×24 小时为你运营虚拟一人公司。

## 功能特性

- **9 人标准团队架构**：预定义角色 — 产品经理、架构师、全栈工程师、UI/UX、QA、运维、市场营销、行政、巡检哨兵
- **可插拔任务引擎**：通过配置切换任务后端（SQLite、GitHub Projects、Plane、Notion）— 无需重写 Agent 逻辑
- **原子化任务认领**：SQLite WAL 模式 + UNIQUE 约束 — 多 Agent 并行无冲突
- **标准化生命周期**：Backlog → Claimed → Req. Confirmed → In Development → In Testing → Bug Open → Released
- **Pull + Push 双模调度**：REST Pull + WebSocket Push，自动降级
- **多 AI 客户端支持**：Claude Code CLI、TRAE、OpenCode、Codex、Qoder
- **三实体认证体系**：管理员 JWT、实例管理者令牌、工作实例令牌
- **Rust + Tauri v2 客户端**：CLI + GUI 桌面应用管理工作实例
- **Docker 部署**：控制中心以 Docker 容器分发

## 下载

| 组件 | 下载 | 平台 |
|------|------|------|
| 工作实例客户端 (macOS) | [最新版本](https://gitee.com/KylinLab/CeXia-App/releases/latest) | macOS 11+ |
| 控制中心 (Docker) | `docker pull crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest` | 任意平台 |

## 快速开始

### 控制中心 (Docker)

```bash
docker pull crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest
docker run -d --name cexia-control-center \
  -p 8080:8080 -p 8000:8000 \
  -v ~/cexia-data:/app/data \
  -e JWT_SECRET_KEY=your-random-secret-key \
  crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest
```

打开 http://localhost:8080，使用 `admin` / `cexia123` 登录（首次登录需修改密码）。

### 工作实例客户端 (macOS)

1. 从 [最新版本](https://gitee.com/KylinLab/CeXia-App/releases/latest) 下载 DMG
2. 挂载 DMG 并拖入 Applications
3. 启动 CeXia Instance
4. 以实例管理者身份登录（默认：`manager` / `manager123`）
5. 注册各角色的工作实例

## 文档

- [用户手册](./user_manual/user_manual.zh.md)
- [演示](./demo/demo.zh.md)

## 联系方式

kylinlab.tech