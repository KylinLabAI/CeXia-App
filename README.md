# CeXia

[中文介绍](README.zh.md)

![CeXia Logo](https://raw.githubusercontent.com/KylinLabAI/CeXia-App/master/resources/logo_256.png)

Intelligent AI task collaboration & scheduling platform — run your virtual one-person company with 9 specialized AI agents working 24/7.

## Features

- **9-Agent Standard Team**: Pre-defined roles — Product Manager, Architect, Full-Stack Engineer, UI/UX, QA, Operations, Marketing, Admin, Sentinel
- **Pluggable Task Engine**: Swap task backends (SQLite, GitHub Projects, Plane, Notion) via config — zero agent rewrites
- **Atomic Task Claiming**: SQLite WAL mode with unique constraints — no duplicate work across parallel agents
- **Standardized Lifecycle**: Backlog → Claimed → Req. Confirmed → In Development → In Testing → Bug Open → Released
- **Pull + Push Dispatch**: REST Pull + WebSocket Push with auto-fallback
- **Multi-AI Client Support**: Claude Code CLI, TRAE, OpenCode, Codex, Qoder
- **Three-Entity Authentication**: Admin JWT, Manager token, Instance token
- **Rust + Tauri v2 Client**: CLI + GUI desktop application for work instance management
- **Docker Deployment**: Control Center distributed as a Docker container

## Download

| Component | Download | Platform |
|-----------|----------|----------|
| Work Instance Client (macOS) | [Latest Release](https://github.com/KylinLabAI/CeXia-App/releases/latest) | macOS 11+ |
| Control Center (Docker) | `docker pull crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest` | Any |

## Quick Start

### Control Center (Docker)

```bash
docker pull crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest
docker run -d --name cexia-control-center \
  -p 8080:8080 -p 8000:8000 \
  -v ~/cexia-data:/app/data \
  -e JWT_SECRET_KEY=your-random-secret-key \
  crpi-5w5kegfxurclu2lz.cn-hangzhou.personal.cr.aliyuncs.com/kylinlab2026/cexia-control-center:latest
```

Open http://localhost:8080 and log in with `admin` / `cexia123` (change password on first login).

### Work Instance Client (macOS)

1. Download the DMG from [Latest Release](https://github.com/KylinLabAI/CeXia-App/releases/latest)
2. Mount the DMG and drag to Applications
3. Launch CeXia Instance
4. Log in as Instance Manager (default: `manager` / `manager123`)
5. Register work instances for your agent roles

## Documentation

- [User Manual](./user_manual/user_manual.md)
- [Demo](./demo/demo.md)

## Contact

kylinlab.tech