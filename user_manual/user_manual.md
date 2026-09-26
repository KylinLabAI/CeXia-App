# CeXia (策匣) — User Manual

**Version**: 1.0.0
**For**: Founders running their virtual company with CeXia

---

## Table of Contents

1. [What CeXia Does](#1-what-cexia-does)
2. [Getting Started](#2-getting-started)
3. [WebUI Walkthrough](#3-webui-walkthrough)
4. [Managing Your Agent Team](#4-managing-your-agent-team)
5. [Task Lifecycle](#5-task-lifecycle)
6. [Settings & Configuration](#6-settings--configuration)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. What CeXia Does

CeXia (策匣) runs your **Virtual One-Person Company**. You — the founder — create tasks and set priorities. A team of AI-powered agents works 24/7 to execute them.

**Your role**: Review the board, create work, approve new agents, make strategic decisions.

**The agents' role**: Claim tasks, execute them, report results. No micromanagement needed.

### The 9 Agent Roles

| Role | What it does for you |
|------|---------------------|
| **Product Manager** | Writes PRDs, manages the backlog, defines acceptance criteria |
| **Architecture Engineer** | Designs system architecture, selects tech stack |
| **Full-Stack Engineer** | Implements features, fixes bugs — can run multiple copies in parallel |
| **UI/UX Designer** | Creates designs, wireframes, product copy |
| **QA Engineer** | Runs tests, reports bugs, validates releases |
| **Operations** | Monitors systems, analyzes data, runs pipelines |
| **Marketing** | Creates content, manages campaigns, drives acquisition |
| **Admin & Finance** | Generates reports, tracks costs, monitors system health |
| **Sentinel** | Cleans up stale locks, audits operations, recovers from failures |

### How It Works (30-second version)

```
1. You create a task in the WebUI         →  appears in the Backlog
2. An available agent claims it            →  moves to Claimed
3. The agent works on it (code/design/QA)  →  progresses through statuses
4. Result lands on the board               →  Released (done) or Bug Open (needs fix)
5. You review anytime                      →  all actions logged, nothing lost
```

---

## 2. Getting Started

### 2.1 What You Need

- A machine to run the Control Center (Linux, macOS, or Windows)
- Docker installed (recommended) — OR Python 3.10+ for direct setup
- A modern web browser (Chrome, Firefox, Edge, Safari)

### 2.2 Launch the Control Center

**Option A — Docker (recommended, one command)**

Pull and run the official Docker image:

```bash
docker pull crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest

docker run -d \
  --name cexia-control-center \
  -p 8080:8080 \
  -p 8000:8000 \
  -v ~/cexia-data:/app/data \
  -e JWT_SECRET_KEY=your-random-secret-key \
  crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest
```

The Control Center starts at **http://localhost:8080** (WebUI) and **http://localhost:8000** (API). Open the WebUI URL in your browser.

Your data (tasks, agent logs, settings) is stored persistently in `~/cexia-data` — it survives restarts and upgrades.

**Option B — Docker Compose**

If you have a `docker-compose.yml` file:

```bash
docker compose up -d
```

**Option C — Pre-configured package**

Your team may provide a pre-configured package. Unzip it, run the launch script, and open your browser to the URL shown.

### 2.3 First Login

1. Open the WebUI in your browser at **http://localhost:8080**
2. Log in with the default credentials:
   - **Username**: `admin`
   - **Password**: `cexia123`
3. **You will be immediately prompted to change your password** — this is required for security. The Control Center will not function until you set a new password.
4. After changing your password, the system initializes and you'll see the **Dashboard**. You're ready to go.

### 2.4 Instance Manager Login (CLI/GUI)

For managing work instances via CLI or GUI, you need an Instance Manager account:

1. Default Manager credentials:
   - **Username**: `manager`
   - **Password**: `manager123`
2. Log in via CLI: `cexia-instance login`
3. Or log in via GUI: App tab → Login form
4. **Change the default password immediately** — Admin should create dedicated Manager accounts for production use

### 2.5 Connect Your First Agent

Agents are work instances running on your machines. Your team sets them up and registers them with the Control Center. After registration:

1. Go to **Instances** in the sidebar
2. Find the new instance (marked **PENDING**)
3. Click **Approve** — the agent can now claim tasks

Repeat for each agent. You can run multiple copies of the same role (e.g., two Full-Stack Engineers) for more throughput.

**Instance Registration Flow:**
1. Instance Manager logs in via CLI/GUI
2. Manager registers a work instance: `cexia-instance register --name Jack --role agent-fullstack`
3. Instance receives access token (`cxt_...`) and sends registration request
4. Admin approves in WebUI → Instance can now claim tasks

---

## 3. WebUI Walkthrough

### 3.1 Dashboard

The Dashboard gives you an instant health check:

- **Total Tasks** — all tasks in the system
- **Online Instances** — agents currently active and connected
- **Completed This Week** — tasks finished in the last 7 days
- **Expired Locks Today** — tasks that timed out (agents may have crashed)

Below the stat cards: **Tasks by Status** (progress bars) and **Tasks by Role** (table). Use these to spot bottlenecks — e.g., too many tasks in Testing, not enough QA agents online.

### 3.2 Task Board

This is where you manage work. Tasks are organized as a **Kanban board** with columns for each status:

`Backlog → Claimed → Req. Confirmed → In Development → In Testing → Bug Open → Released`

**To create a task:**

1. Click **+ Create Task** (top-right)
2. Fill in the form:
   - **Title** — a one-line summary (required)
   - **Description** — details, acceptance criteria, links
   - **Agent Role** — who should handle this (leave blank for any)
   - **Priority** — Urgent / High / Medium / Low
   - **Severity** — Critical / Major / Minor / Trivial
3. Click **Create**

The card appears in the Backlog column. Agents matching the role will pick it up automatically.

**To view a task:** Click any card. A side panel opens showing all details — status, assigned agent, priority, full description.

### 3.3 Audit Logs

Every action by every agent is recorded. Go to **Audit Logs** to see:

- Which agent did what
- When it happened
- What changed (status transitions, errors)

You can filter by agent name, action type, or time period. Use this to investigate issues or review agent activity.

---

## 4. Managing Your Agent Team

### 4.1 The Instances Page

Go to **Instances** to see all registered agents:

| Column | Meaning |
|--------|---------|
| **Name** | The agent's name (e.g., "Jack") |
| **Role** | What the agent does (e.g., Full-Stack Engineer) |
| **Status** | Green = online and working. Grey = offline or disconnected |
| **Approved** | Green = active. Yellow = waiting for your approval |

### 4.2 Approving New Agents

When your team registers a new agent:

1. It appears in the table with **PENDING** status
2. Click **Approve** to activate it
3. The agent can now claim tasks

### 4.3 Revoking Access

If an agent should stop working:

1. Find it in the table
2. Click **Revoke**
3. The agent loses access immediately — its next request will be rejected

You can re-register it later if needed.

### 4.4 Scaling Up

Need more development throughput? Have your team register another Full-Stack Engineer agent on another machine. Approve it in the WebUI. Both agents will work in parallel, each claiming separate tasks — no conflicts, no duplicates.

---

## 5. Task Lifecycle

### 5.1 How a Task Moves Through the System

```
Backlog               ← You create a task here
   ↓  (agent claims it)
Claimed               ← An agent owns it now
   ↓  (agent confirms the spec)
Requirements Confirmed
   ↓  (agent starts building)
In Development
   ↓  (agent finishes, hands off to QA)
In Testing
   ↓  ↙
   ↓   Tests fail → Bug Open → back to In Development (for fixes)
   ↓
Released              ← Done! Task complete
```

### 5.2 What You Need to Know

- **You don't need to move tasks manually** — agents handle state transitions automatically
- **You CAN create tasks directly** — use the +Create Task button anytime
- **Stuck tasks recover automatically** — if an agent crashes, a Sentinel process releases the task back to Backlog after a timeout (default: 2 hours)
- **Multiple agents can't grab the same task** — the system guarantees only one agent claims each task

### 5.3 Priority & Severity

| Field | What it means | Values |
|-------|--------------|--------|
| **Priority** | How urgent this is for the business | Urgent → High → Medium → Low |
| **Severity** | How bad the issue is (for bugs) | Critical → Major → Minor → Trivial |

Agents pick up higher-priority tasks first. Set Priority to **Urgent** for tasks that need immediate attention.

---

## 6. Settings & Configuration

All settings are in **WebUI → Settings**. Changes take effect immediately — no restart.

### 6.1 Task Storage

| Backend | Best for | Requires |
|---------|----------|----------|
| **Built-In** (default) | Getting started, single-machine use | Nothing — works out of the box |
| **GitHub Projects** | Teams already using GitHub, public visibility | GitHub account + project board setup |

Switch backends anytime. Tasks in the Built-In storage stay there when you switch to GitHub, and vice versa.

### 6.2 AI Model Configuration

Configure AI model access for work instances:

| Setting | Description |
|---------|-------------|
| **API Key** | AI model API key (stored securely, masked in UI) |
| **Base URL** | AI model API endpoint |
| **Default Model** | Default model for new instances |

Work instances receive model credentials from the Control Center — they don't store them locally.

### 6.3 Scheduling Parameters

| Setting | Default | What it does |
|---------|---------|-------------|
| **Lock Expiry** | 2 hours | How long an agent can hold a task before it auto-releases |
| **Sentinel Interval** | 60 seconds | How often the system checks for stuck/expired tasks |
| **Heartbeat Timeout** | 120 seconds | Time without a ping before marking an agent offline |
| **Pull Interval** | 30 seconds | How often agents check for new tasks (when not using push) |

Defaults work well for most cases. Adjust Lock Expiry if your agents work on very long or very short tasks.

---

## 7. Troubleshooting

### "No tasks appear on the board"

- Did you create any? Click **+ Create Task** to add one.
- If using GitHub Projects: check that the connection settings are correct (Settings page).
- Try refreshing the page.

### "An agent can't pick up tasks"

- Check **Instances** — is the agent Approved and Online?
- Does the task have an Agent Role set? If so, only agents with that role can claim it. Clear the role field to let any agent claim it.

### "A task is stuck in Claimed status"

- The agent that claimed it may have stopped unexpectedly.
- The Sentinel process will auto-release it after the Lock Expiry period (default 2 hours).
- If you need it released sooner, ask your team to restart the Control Center.

### "An agent shows as OFFLINE but it should be working"

- The agent's heartbeat may have timed out (default: 120 seconds without contact).
- The agent will reconnect and go back to ONLINE automatically.
- If it stays OFFLINE, ask your team to check the agent's machine and logs.

### "I can't log in"

- Default credentials: Username `admin`, Password `cexia123`. If this is your first time, use these.
- If you've already changed the password and forgot it, ask your team to reset it.
- Check you're using the correct URL.

### "Something else is wrong"

All system activity is in **Audit Logs** — start there to see what happened. If you need deeper investigation, your team can check the system logs on the server.

---

**That's it — you now know everything needed to run your virtual company with CeXia.** Create tasks, approve agents, check the dashboard, and let the agents handle the rest.
