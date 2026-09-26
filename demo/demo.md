# CeXia Demo: From Zero to AI-Driven Production

[中文演示](demo.zh.md)

This demo walks through the complete CeXia workflow — from setting up your first Instance Manager account to running a multi-agent team that turns an idea into production code.

---

## Phase 1 — Create Instance Manager Account

Create an **Instance Manager** account in the CeXia backend (Control Center WebUI). This account is used to log in to the **CeXia Instance** desktop client and manage local work instances.

![Create manager account](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/1.0_create_manager_account_in_backend.png)

> The admin fills in **Username**, **Password**, and **Display Name**, then clicks **Create**. The Display Name identifies this workstation (e.g., "Kylin MacBookPro").

---

## Phase 2 — Configure Global Environment

Launch the **CeXia Instance** client (Work Instance Manager) and configure the shared settings that all instances on this workstation will inherit.

### 2.1 Login & Global Config

Log in with the account created in Phase 1, then set up:

- **Default AI Client & Model** — e.g., `ClaudeCode` / `deepseek-v4-pro` with API base URL
- **App-Level Repos (Shared)** — resource repos (like `KylinAgents`) that are symlinked into every instance's workspace automatically
- **Control Center Servers** — the backend URL(s) instances will register with

![Login and global config](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/2.0_login_ai_repo_config.png)

> All new instances inherit these defaults. Per-instance overrides are configured later in each instance's Settings tab.

---

## Phase 3 — Create Instances (Role-Based)

Each **Instance** maps to one CeXia agent role (e.g., Architect, PM, UI/UX, Fullstack). Instances bind role-specific resources (agents, skills, workflows, tools, knowledge) and run as independent worker processes.

### 3.1 Create the First Instance

Click **+ New instance**, give it a name, select a **Role**, and choose the target Control Center.

![Create new instance](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.0_create_new_instance.png)

> Example: Instance **"Jack"** with role **Architect (`agent-arch`)** connecting to `http://localhost:8000`.

### 3.2 Review Auto-Bound Resources

Once created, the instance automatically binds resources defined for its role. Open the **Resources** tab to inspect:

- **Agents** — e.g., `engineering-architecture`
- **Skills** — e.g., `core-module-designer`, `repo-app-creator`, `repo-quality-assessment`
- **Workflows** — e.g., `main_workflow`, `stage-b-architecture`, `stage-g-repo-scaffolding`
- **Knowledge** — e.g., `engineering-architecture`

![Instance resources - Architect role](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.1_new_instance_resources_architecture_role.png)

> Same-role instances share the same repos and their resources via symbolic links.

### 3.3 Configure Per-Instance AI API Key

Open the **Settings** tab to set the AI model credentials for this specific instance:

- **AI Client / Model** — inherited from global config or overridden here
- **API base URL** — e.g., `https://api.deepseek.com/v1`
- **API key** — stored locally; masked after save

![Set AI API key per instance](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/3.2_new_instance_setting_ai_api_key.png)

---

## Phase 4 — Create More Instances for Different Roles

Repeat the create-instance process for each role in your team. Each role gets its own resource bindings and (optionally) its own AI API key.

### 4.1 Multi-Instance Overview

The **Instances** list shows all configured work instances on this workstation, with columns for Role, Registration status, Runtime state, Bindings count, and actions.

![Multiple instances list](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.0_more_instances.png)

> Example setup: **Jack** (arch), **Jane** (pm), **Lily** (uiux), **Tom** (fullstack) — all on the same workstation.

### 4.2 Role-Specific Resource Bindings

Different roles bind completely different resources. Compare the **PM** role resources below with the Architect resources in 3.2:

- **Agent**: `product-program-manager`
- **Skills**: `app-config-initializer`, `app-draft-info-creator`, `app-draft-introduce-creator`, `app-draft-naming`, `requirement-writer`
- **Workflows**: `app-document-workflow`, `main_workflow`, `stage-a`
- **Knowledge**: `product-program-manager`

![Instance resources - PM role](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.1_new_instance_resources_pm_role.png)

### 4.3 Role-Based API Keys (Optional Security)

For cost control and access isolation, create separate API keys per role in your AI platform backend (e.g., DeepSeek). Each instance can use a different key:

![Role-based API keys in DeepSeek platform](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/4.2_deepseek_platform_different_role_use_diffrent_key.png)

> Example keys: `role-UIDesigner`, `role-architecture`, `role-pm`, `role-dev-engineer`.

---

## Phase 5 — Register & Start Worker Instances

Before instances can pull and execute tasks, they must register with the Control Center and be approved by the admin.

### 5.1 Send Register Request

For each instance, click **Register** in the Actions column. The instance sends a registration request to the Control Center with its name, role, host, and OS info.

![Register request sent](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.1_regsiter_request.png)

> After registration, the status changes from "not registered" to "**registered**" with an assigned Instance ID and Access Token.

### 5.2 Admin Approves Registration

In the CeXia backend WebUI (**Instance Management** page), the admin reviews pending registrations and clicks **Approve** (or **Config** to adjust settings first).

![Admin approves registration](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.2_admin_approve_register.png)

> All four instances (Tom, Lily, Jane, Jack) show **PENDING** status before approval. Approved instances become active workers.

### 5.3 Start Worker Instances

Once approved, click **Start** on each instance. The worker process begins and auto-pulls tasks from the backend that match its role.

![Start worker instance](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.3_start_worker_instance.png)

> Runtime status changes from "stopped" to "**idle**" (ready) or "busy" (executing a task).

### 5.4 Worker Instances Running

All registered instances are now running as background processes, each pulling tasks independently based on its role assignment.

![Worker instances processing](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/5.4_worker_instances_process.png)

> Terminal output confirms each instance process (Jack, Jane, Lily, Tom) started successfully.

---

## Phase 6 — From Idea to Production

With the multi-agent team online, you can now drive a project from idea to production through the CeXia workflow engine.

### 6.1 Create Project

In the CeXia backend WebUI, create a new **Project** with:

- **Name** — project identifier
- **Description** — what the project is about
- **Repository Links**:
  - **Source Code Repo URL** — e.g., `https://gitee.com/KylinLab/YinXia`
  - **Engineering Doc Repo URL + Path** — where engineering docs live
  - **Production Doc Repo URL + Path** — where published docs go

![Create project](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/6.1_create_project.png)

> Repository links let agents read/write docs and source code directly through the workflow.

### 6.2 Create First Task: Idea → Requirements

Create a task to kick off the workflow loop:

- **Title** — e.g., "Ideas to requirements"
- **Description** — instruct the agent which doc to read and what to produce
- **Task Type** — e.g., "Requirement Analysis"
- **Project** — select the project
- **Agent Role** — e.g., **PM** (routes to Jane's instance)
- **Priority / Severity** — e.g., Urgent / Critical

![Idea to requirements task](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/6.2_create_task_idea_to_requirements.png)

> The PM agent reads `draft_idea.md`, writes/updates `requirement.md` in engineering docs, then commits and pushes. Downstream tasks (Architecture → Implementation → QA → Release) follow automatically via the workflow definition.

---

## Whole Workflow Execution

![Whole workflow execution](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/demo/resources/7.0_idea_to_requirements.svg)

## What Humans Do

The AI agents handle the execution loop. Your role as the human orchestrator is to:

1. **Monitor** — watch task progress, review outputs, check instance health
2. **Improve the workflow** — refine stage definitions, add gates, adjust routing rules
3. **Upgrade agent capabilities** — update guidelines, add skills, enhance tools
4. **Grow the knowledge base** — feed successful patterns back into knowledge repos
5. **Scale** — add more instances, more roles, more projects on the same infrastructure

> CeXia is designed for continuous improvement: better inputs (workflow/skills/tools/knowledge) = better AI performance over time.