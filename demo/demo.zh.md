# 策匣 CeXia 演示：从零到 AI 驱动的生产交付

[English Demo](demo.md)

本演示展示完整的 CeXia 工作流程 — 从创建第一个实例管理者账户到运行多 Agent 团队将想法转化为生产代码。

---

## 阶段一 — 创建实例管理者账户

在 CeXia 后端（控制中心 WebUI）中创建**实例管理者**账户。此账户用于登录 **CeXia Instance** 桌面客户端并管理本地工作实例。

![创建管理者账户](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/1.0_create_manager_account_in_backend.png)

> 管理员填写**用户名**、**密码**和**显示名称**，然后点击**创建**。显示名称标识此工作站（例如 "Kylin MacBookPro"）。

---

## 阶段二 — 配置全局环境

启动 **CeXia Instance** 客户端（工作实例管理器），配置此工作站上所有实例将继承的共享设置。

### 2.1 登录与全局配置

使用阶段一创建的账户登录，然后设置：

- **默认 AI 客户端与模型** — 例如 `ClaudeCode` / `deepseek-v4-pro` 及 API 基础 URL
- **应用级仓库（共享）** — 资源仓库（如 `KylinAgents`）自动通过符号链接挂载到每个实例的工作空间
- **控制中心服务器** — 实例将注册的后端 URL

![登录与全局配置](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/2.0_login_ai_repo_config.png)

> 所有新实例继承这些默认值。每个实例的单独覆盖在各自的设置标签页中配置。

---

## 阶段三 — 创建实例（按角色）

每个**实例**映射到一个 CeXia Agent 角色（如架构师、PM、UI/UX、全栈）。实例绑定角色特定的资源（Agent、技能、工作流、工具、知识）并作为独立工作进程运行。

### 3.1 创建第一个实例

点击 **+ 新建实例**，命名，选择**角色**，选择目标控制中心。

![创建新实例](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.0_create_new_instance.png)

> 示例：实例 **"Jack"**，角色 **架构师（`agent-arch`）**，连接到 `http://localhost:8000`。

### 3.2 查看自动绑定的资源

创建后，实例自动绑定其角色定义的资源。打开**资源**标签页查看：

- **Agent** — 例如 `engineering-architecture`
- **技能** — 例如 `core-module-designer`、`repo-app-creator`、`repo-quality-assessment`
- **工作流** — 例如 `main_workflow`、`stage-b-architecture`、`stage-g-repo-scaffolding`
- **知识库** — 例如 `engineering-architecture`

![实例资源 - 架构师角色](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.1_new_instance_resources_architecture_role.png)

> 同角色实例通过符号链接共享相同的仓库和资源。

### 3.3 配置每个实例的 AI API Key

打开**设置**标签页为此实例设置 AI 模型凭据：

- **AI 客户端 / 模型** — 继承全局配置或在此覆盖
- **API 基础 URL** — 例如 `https://api.deepseek.com/v1`
- **API Key** — 本地存储，保存后脱敏显示

![设置每个实例的 AI API Key](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.2_new_instance_setting_ai_api_key.png)

---

## 阶段四 — 为不同角色创建更多实例

为团队中的每个角色重复创建实例过程。每个角色获得自己的资源绑定和（可选）自己的 AI API Key。

### 4.1 多实例概览

**实例**列表显示此工作站上所有已配置的工作实例，包含角色、注册状态、运行时状态、绑定数量和操作列。

![多实例列表](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.0_more_instances.png)

> 示例设置：**Jack**（架构师）、**Jane**（PM）、**Lily**（UI/UX）、**Tom**（全栈）— 全部在同一工作站上。

### 4.2 角色特定的资源绑定

不同角色绑定完全不同的资源。对比下方 **PM** 角色的资源与 3.2 中的架构师资源：

- **Agent**：`product-program-manager`
- **技能**：`app-config-initializer`、`app-draft-info-creator`、`app-draft-introduce-creator`、`app-draft-naming`、`requirement-writer`
- **工作流**：`app-document-workflow`、`main_workflow`、`stage-a`
- **知识库**：`product-program-manager`

![实例资源 - PM 角色](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.1_new_instance_resources_pm_role.png)

### 4.3 基于角色的 API Key（可选安全措施）

为了成本控制和访问隔离，在 AI 平台后端（如 DeepSeek）为每个角色创建单独的 API Key。每个实例可使用不同的 Key：

![DeepSeek 平台中按角色的 API Key](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.2_deepseek_platform_different_role_use_diffrent_key.png)

> 示例 Key：`role-UIDesigner`、`role-architecture`、`role-pm`、`role-dev-engineer`。

---

## 阶段五 — 注册并启动工作实例

实例在拉取和执行任务之前，必须先向控制中心注册并获得管理员批准。

### 5.1 发送注册请求

对每个实例，在操作列中点击**注册**。实例向控制中心发送注册请求，包含其名称、角色、主机和操作系统信息。

![注册请求已发送](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.1_regsiter_request.png)

> 注册后，状态从"未注册"变为"**已注册**"，并分配实例 ID 和访问令牌。

### 5.2 管理员批准注册

在 CeXia 后端 WebUI（**实例管理**页面），管理员审查待处理的注册并点击**批准**（或先点击**配置**调整设置）。

![管理员批准注册](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.2_admin_approve_register.png)

> 全部四个实例（Tom、Lily、Jane、Jack）批准前显示 **PENDING** 状态。批准的实例成为活跃工作进程。

### 5.3 启动工作实例

批准后，点击每个实例的**启动**。工作进程开始运行，自动从后端拉取匹配其角色的任务。

![启动工作实例](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.3_start_worker_instance.png)

> 运行时状态从"已停止"变为"**空闲**"（就绪）或"忙碌"（执行任务中）。

### 5.4 工作实例运行中

所有已注册实例现在作为后台进程运行，每个实例根据其角色分配独立拉取任务。

![工作实例处理中](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.4_worker_instances_process.png)

> 终端输出确认每个实例进程（Jack、Jane、Lily、Tom）已成功启动。

---

## 阶段六 — 从想法到生产

多 Agent 团队上线后，你现在可以通过 CeXia 工作流引擎驱动项目从想法到生产。

### 6.1 创建项目

在 CeXia 后端 WebUI 中创建新**项目**：

- **名称** — 项目标识
- **描述** — 项目内容
- **仓库链接**：
  - **源码仓库 URL** — 例如 `https://gitee.com/KylinLab/YinXia`
  - **工程文档仓库 URL + 路径** — 工程文档所在位置
  - **产品文档仓库 URL + 路径** — 发布文档所在位置

![创建项目](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/6.1_create_project.png)

> 仓库链接让 Agent 通过工作流直接读写文档和源码。

### 6.2 创建第一个任务：想法 → 需求

创建任务启动工作流循环：

- **标题** — 例如 "想法转需求"
- **描述** — 指示 Agent 读取哪个文档、产出什么
- **任务类型** — 例如 "需求分析"
- **项目** — 选择项目
- **Agent 角色** — 例如 **PM**（路由到 Jane 的实例）
- **优先级 / 严重程度** — 例如 Urgent / Critical

![想法转需求任务](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/6.2_create_task_idea_to_requirements.png)

> PM Agent 读取 `draft_idea.md`，在工程文档中编写/更新 `requirement.md`，然后提交并推送。下游任务（架构 → 实现 → QA → 发布）通过工作流定义自动跟进。

---

## 完整工作流执行

![完整工作流执行](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/7.0_idea_to_requirements.svg)

## 人类做什么

AI Agent 处理执行循环。你作为人类编排者的角色是：

1. **监控** — 观察任务进度、审查输出、检查实例健康状态
2. **改进工作流** — 优化阶段定义、添加门控、调整路由规则
3. **升级 Agent 能力** — 更新指南、添加技能、增强工具
4. **丰富知识库** — 将成功模式反馈到知识仓库
5. **扩展** — 在同一基础设施上添加更多实例、更多角色、更多项目

> CeXia 为持续改进而设计：更好的输入（工作流/技能/工具/知识）= 更好的 AI 表现。