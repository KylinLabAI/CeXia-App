## 策匣 CeXia v1.0.0 — 智能 AI 任务协同调度平台

### 一句话介绍

由 9 个专业化 AI Agent 7×24 小时为你运营虚拟一人公司的智能调度平台。

### 核心亮点

**完整 AI 团队架构**
- 产品经理、架构师、全栈工程师、UI/UX、QA、运维、市场营销、行政、巡检哨兵 — 9 个预定义角色覆盖全流程

**可插拔任务引擎**
- 通过配置切换任务后端（内置 SQLite、GitHub Projects V2、未来 Plane/Notion/Linear）
- 无需重写 Agent 逻辑，无缝迁移

**原子化任务认领**
- SQLite WAL 模式 + UNIQUE 约束
- 多 Agent 并行永无冲突
- 巡检哨兵自动释放过期锁

**Pull + Push 双模调度**
- REST Pull + WebSocket Push
- 自动降级，Agent 始终获取下一个可用任务

**多 AI 客户端支持**
- Claude Code CLI、TRAE、OpenCode、Codex、Qoder

**Rust + Tauri v2 桌面客户端**
- CLI + GUI 原生 macOS 应用

### 适用场景

独立创始人、个人开发者、小团队 — 用 AI Agent 团队替代人工招聘，7×24 小时持续交付。

🔗 下载：https://gitee.com/KylinLab/CeXia-App/releases/tag/v1.0.0