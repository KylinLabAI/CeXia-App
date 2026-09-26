## 策匣 CeXia v1.0.0 发布：用 AI Agent 团队运营你的虚拟一人公司

### 这是什么

策匣 CeXia 是一个智能 AI 任务协同调度平台，让独立创始人以完整跨职能团队的方式运营。你负责战略决策，9 个专业化 AI Agent 7×24 小时执行日常交付。

### 技术架构

**控制中心（Server）**
- FastAPI + Vue 3 + Element Plus + SQLite
- 三实体认证体系：管理员（JWT）、实例管理者（`imt_` 令牌）、工作实例（`cxt_` 令牌）
- 可插拔抽象任务引擎：内置 SQLite 驱动 + GitHub Projects V2 驱动
- Docker 容器化部署

**工作实例（Client）**
- Rust + Tauri v2 桌面应用
- CLI + GUI 双界面
- 支持多种 AI 客户端：Claude Code CLI、TRAE、OpenCode、Codex、Qoder

### 核心机制

- **原子化任务认领**：SQLite WAL 模式 + UNIQUE 约束，多 Agent 并行无冲突
- **标准化生命周期**：Backlog → Claimed → 需求确认 → 开发中 → 测试中 → Bug 开启 → 已发布
- **Pull + Push 双模调度**：WebSocket 推送 + REST 拉取自动降级

### 为什么选择 CeXia

与通用 AI 编程助手不同，CeXia 提供完整的团队架构和角色定义。每个 Agent 通过结构化任务记录通信，消除歧义和竞态条件。平台为持续改进而设计：更好的输入（工作流、技能、工具、知识）= 更好的 AI 表现。

🔗 下载：https://gitee.com/KylinLab/CeXia-App/releases/tag/v1.0.0