<div align="center">

# ðŸ§ LinuxPilot AI

**A local, safety-first AI-powered Linux operations assistant and intelligent system copilot.**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Ollama](https://img.shields.io/badge/Qwen-2.5:7B-FF6B6B?style=flat-square)](https://ollama.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-55%20passed-brightgreen?style=flat-square&logo=pytest)](tests/)

<br/>

> LinuxPilot AI is not a generic chat wrapper around a shell. It is an **intelligent, safety-first Linux operations agent** â€” a deterministic pipeline that classifies intent, generates task plans, collects real system metrics, validates commands through a **3-tier safety layer**, and synthesizes structured, actionable insights in milliseconds.

<br/>

[ðŸš€ Quick Start](#-quick-start-for-linux) Â· [ðŸ“– API Reference](#-api-reference) Â· [ðŸ›¡ï¸ Safety Layer](#-3-tier-command-safety-layer) Â· [âš¡ Performance](#-performance--benchmarks) Â· [ðŸ§ª Tests](#-running-tests)

</div>

---

## ðŸ—ï¸ Architecture Overview

```
Conventional AI Terminals:   User Prompt â”€â”€â–º LLM â”€â”€â–º Raw Shell Execution   âŒ Dangerous & Unpredictable

LinuxPilot AI Pipeline:

  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚                  User Natural Language Query                    â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚  Intent Classifier (Deterministic Fast-Path + Qwen 2.5 Fallback)â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚         Task Planner  (Deterministic & Contextual Workflows)    â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚     Tool Registry  (psutil Â· os.scandir Â· systemctl Â· etc.)    â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚      3-Tier Command Safety Validator                            â”‚
  â”‚      READ_ONLY â”€â”€â–º MODIFYING â”€â”€â–º DANGEROUS                     â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚         Structured Execution & Response Synthesis               â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                 â”‚
                                 â–¼
  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
  â”‚         React 18 + TypeScript Dashboard UI                      â”‚
  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

---

## âœ¨ Key Features

| Feature | Description |
|---|---|
| âš¡ **Instant Diagnostics** | Live CPU, per-core utilization, 1m/5m load averages, RAM & swap, disk, network |
| ðŸ“‚ **High-Speed File Discovery** | Deep filesystem traversal via `os.scandir`, extension filters, size thresholds |
| âš™ï¸ **Systemd Service Management** | Safely inspect & control nginx, docker, ssh, apache2, postgresql, mysql |
| ðŸ“œ **Log Analysis** | Structured `journalctl` & `dmesg` queries with priority filtering |
| ðŸ’¡ **Linux Concept Tutor** | Instant permission explanations (`chmod 755`), tarball usage, command breakdowns |
| ðŸ”’ **Local-Only Security** | Backend bound to `127.0.0.1` â€” no unauthorized network access |
| ðŸ–¥ï¸ **Modern Dashboard** | React 18 + TypeScript + Tailwind: live metrics, pipeline visualization, query history |
| ðŸ¤– **AI-Powered Fallback** | Qwen 2.5:7B via Ollama for complex or ambiguous queries beyond the fast path |
| ðŸ§ª **55 Automated Tests** | Full test suite covering API, intent, safety, orchestration, and tools |

---

## âš¡ Performance & Benchmarks

LinuxPilot AI uses a **Deterministic Fast-Path Architecture** that bypasses LLM roundtrips for standard queries, reserving Ollama only for genuinely ambiguous inputs.

| Query / Operation | Before | After | Speedup |
|---|---|---|---|
| `"Why is my computer running slowly?"` | ~45,000 ms | **506 ms** | **89Ã— faster** |
| `"Find all large files in my home directory"` | ~164,000 ms | **73 ms** | **2,200Ã— faster** |
| `"Find Python files larger than 50 MB"` | ~120,000 ms | **50 ms** | **2,400Ã— faster** |
| `"Show me the status of nginx"` | ~30,000 ms | **8 ms** | **3,750Ã— faster** |
| `"Show recent system errors"` | ~25,000 ms | **16 ms** | **1,560Ã— faster** |
| `"Explain what chmod 755 means"` | ~15,000 ms | **1 ms** | **15,000Ã— faster** |
| `"df -h"` (read-only execution) | ~15,000 ms | **10 ms** | **1,500Ã— faster** |
| `"systemctl restart nginx"` (confirmation gate) | ~20,000 ms | **< 1 ms** | **20,000Ã— faster** |
| `"rm -rf /"` (blocked by safety engine) | ~10,000 ms | **2 ms** | **5,000Ã— faster** |

---

## ðŸ›¡ï¸ 3-Tier Command Safety Layer

Security is the **core architectural foundation** of LinuxPilot AI. Every command passes through a strict 3-tier validation boundary before any execution occurs.

```
                    â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
                    â”‚     User Request / Agent Command     â”‚
                    â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                                       â”‚
                           Command Validation Layer
                                       â”‚
          â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
          â–¼                            â–¼                            â–¼
     [READ_ONLY]                  [MODIFYING]                 [DANGEROUS]
  Non-destructive              State-altering changes      Catastrophic deletion
  (df, free, ps, top,         (systemctl restart,          (rm -rf /, mkfs,
   ls, uptime, status)         apt install, chmod)          fork bombs, curl|bash)
          â”‚                            â”‚                            â”‚
          â–¼                            â–¼                            â–¼
    AUTO-EXECUTE              EXPLICIT USER CONFIRMATION    PERMANENTLY BLOCKED
   (Instant Output)            REQUIRED before action        (Zero Exceptions)
```

> **âš ï¸ Safety Guarantee:** Dangerous commands (`rm -rf /`, raw disk overwriting, fork bombs) are blocked **unconditionally**. Passing `confirmed=True` will **never** bypass a `BLOCKED` verdict.

---

## ðŸš€ Quick Start for Linux

### Prerequisites

- Linux OS â€” Ubuntu 20.04+ Â· Debian 11+ Â· Fedora 38+ Â· Linux Mint
- Python 3.10+ & `python3-venv`
- Node.js 18+ & `npm`
- Git
- [Ollama](https://ollama.ai) with `qwen2.5:7b-instruct` pulled *(optional â€” only needed for complex queries)*

### 1. Clone the Repository

```bash
git clone https://github.com/divyamsingh21/LinuxPilot-Ai.git
cd LinuxPilot-Ai
```

### 2. One-Command Automated Install

```bash
chmod +x scripts/install.sh
./scripts/install.sh
```

The installer automatically:
1. âœ… Verifies Python 3.10+ and Node.js 18+
2. âœ… Creates a clean `.venv/` virtual environment
3. âœ… Installs all backend dependencies (`requirements.txt`)
4. âœ… Installs frontend npm packages
5. âœ… Initializes the SQLite database schema

### 3. Configure Environment

```bash
cp .env.example .env
# Edit .env to customize Ollama host, model, or safety settings
```

### 4. Launch LinuxPilot AI

```bash
./scripts/start.sh
```

| Service | URL |
|---|---|
| ðŸ–¥ï¸ Dashboard UI | http://localhost:1420 |
| ðŸ”Œ Backend API | http://127.0.0.1:8000 |
| ðŸ“š Swagger Docs | http://127.0.0.1:8000/docs |

### 5. Management Commands

```bash
./scripts/status.sh   # Check service health
./scripts/stop.sh     # Stop all services cleanly
```

---

## ðŸªŸ Windows (Development & Testing)

LinuxPilot AI supports Windows for dashboard development and testing. Linux-native integrations (`systemctl`, `journalctl`) return structured status messages on Windows.

```powershell
# Terminal 1 â€” Backend
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt
uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000

# Terminal 2 â€” Frontend
cd frontend
npm install
npm run dev
```

---

## ðŸ“ Project Structure

```
LinuxPilot-Ai/
â”œâ”€â”€ backend/                    # FastAPI Python backend
â”‚   â”œâ”€â”€ ai/                     # Intent classifier, Ollama client, prompts
â”‚   â”œâ”€â”€ agent/                  # Orchestrator & planner
â”‚   â”œâ”€â”€ api/                    # Route handlers (agent, diagnostics, services, logs, etc.)
â”‚   â”œâ”€â”€ commands/               # Command execution & safety validator
â”‚   â”œâ”€â”€ database/               # SQLite schema & session management
â”‚   â”œâ”€â”€ diagnostics/            # CPU, memory, disk, network tools
â”‚   â”œâ”€â”€ search/                 # High-speed file search engine
â”‚   â”œâ”€â”€ services/               # Systemd service manager
â”‚   â”œâ”€â”€ utils/                  # Config, logger, helpers
â”‚   â”œâ”€â”€ validator/              # 3-tier command safety layer
â”‚   â””â”€â”€ main.py                 # FastAPI application entrypoint
â”œâ”€â”€ frontend/                   # React 18 + TypeScript + Vite + Tailwind UI
â”‚   â”œâ”€â”€ src/
â”‚   â”‚   â”œâ”€â”€ components/         # UI components (dashboard, chat, metrics)
â”‚   â”‚   â”œâ”€â”€ hooks/              # Custom React hooks
â”‚   â”‚   â””â”€â”€ services/           # API client services
â”‚   â””â”€â”€ src-tauri/              # Tauri desktop app wrapper (optional)
â”œâ”€â”€ tests/                      # 55 automated pytest tests
â”œâ”€â”€ scripts/                    # install.sh, start.sh, stop.sh, status.sh
â”œâ”€â”€ docker/                     # Docker configuration
â”œâ”€â”€ docker-compose.yml          # Multi-container orchestration
â”œâ”€â”€ .env.example                # Environment variable template
â””â”€â”€ requirements.txt            # Python dependencies
```

---

## ðŸ“¡ API Reference

| Endpoint | Method | Description |
|---|---|---|
| `/api/health` | `GET` | Health check and environment configuration |
| `/api/agent/ask` | `POST` | Full pipeline: classify â†’ plan â†’ execute â†’ synthesize |
| `/api/agent/history` | `GET` | Recent interaction history from SQLite |
| `/api/intent/classify` | `POST` | Intent detection & parameter extraction |
| `/api/diagnostics/cpu` | `GET` | Real-time CPU usage, core breakdown, load average |
| `/api/diagnostics/memory` | `GET` | RAM and swap utilization |
| `/api/diagnostics/disk` | `GET` | Mount point capacity & usage |
| `/api/diagnostics/network` | `GET` | Gateway, DNS, IP, and connectivity status |
| `/api/services/{name}/status` | `GET` | Inspect systemd service status |
| `/api/services/{name}/restart` | `POST` | Restart service (requires user confirmation) |
| `/api/logs/journalctl` | `POST` | Safe parameterized journalctl query |
| `/api/logs/dmesg` | `POST` | Parameterized kernel dmesg query |
| `/api/search/files` | `POST` | Fast filesystem search by name, category, size |
| `/api/execute/command` | `POST` | Validate & run command via 3-tier safety layer |

> **Interactive Swagger UI** available at `http://127.0.0.1:8000/docs` when the backend is running.

---

## ðŸ§ª Running Tests

```bash
# From project root â€” runs all 55 tests
python -m pytest -v
```

```
tests/test_api.py                 (9 tests)  âœ… PASSED
tests/test_command_safety.py      (4 tests)  âœ… PASSED
tests/test_command_validator.py  (13 tests)  âœ… PASSED
tests/test_intent_classifier.py   (7 tests)  âœ… PASSED
tests/test_orchestrator.py        (9 tests)  âœ… PASSED
tests/test_planner.py             (6 tests)  âœ… PASSED
tests/test_tools.py               (7 tests)  âœ… PASSED
â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•â•
55 passed in 2.72s
```

---

## ðŸ³ Docker Support

```bash
# Launch full stack with Docker Compose
docker-compose up --build

# Run backend only
docker-compose up backend
```

---

## âš™ï¸ Environment Configuration

Copy `.env.example` to `.env` and configure:

```env
# AI / Ollama
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=qwen2.5:7b-instruct

# Application
APP_ENV=development
LOG_LEVEL=INFO
API_HOST=127.0.0.1
API_PORT=8000

# Database
DATABASE_URL=sqlite:///./linuxpilot.db

# Safety (read carefully before enabling!)
ALLOW_COMMAND_EXECUTION=false
ALLOWED_SERVICES=docker,apache2,nginx,ssh,mysql,postgresql
COMMAND_TIMEOUT_SECONDS=20
```

> **âš ï¸ Warning:** Keep `ALLOW_COMMAND_EXECUTION=false` until you have reviewed the command validation layer and understand its behavior.

---

## ðŸŽ¯ Demo Walkthrough

Try these queries in the dashboard for a rapid feature tour:

1. **âš¡ Live Diagnostics** â€” `"Why is my computer running slowly?"` â†’ real-time CPU, RAM, disk in ~500 ms
2. **ðŸ” File Search** â€” `"Find all large files in my home directory"` â†’ files >100 MB ranked in ~70 ms
3. **ðŸ Filtered Search** â€” `"Find Python files larger than 50 MB"` â†’ parameter extraction demo
4. **âš ï¸ Modifying Command** â€” `"Restart nginx"` â†’ watch the confirmation gate in action
5. **ðŸš« Safety Block** â€” `"rm -rf /"` â†’ immediate `<2 ms` blocked response
6. **ðŸ’¡ Concept Tutor** â€” `"Explain chmod 755"` â†’ instant permission breakdown table

---

## ðŸ§° Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Python 3.10+, FastAPI 0.115, Uvicorn, Pydantic v2 |
| **AI / LLM** | Ollama + Qwen 2.5:7B-Instruct (local, offline-capable) |
| **System Tools** | psutil, os.scandir, systemctl, journalctl, dmesg |
| **Frontend** | React 18, TypeScript, Vite, Tailwind CSS |
| **Desktop** | Tauri (optional cross-platform wrapper) |
| **Database** | SQLite (interaction history) |
| **Testing** | pytest, pytest-asyncio |
| **DevOps** | Docker, Docker Compose |

---

## ðŸ¤ Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'feat: add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

Please ensure all 55 tests pass before submitting a PR: `python -m pytest -v`

---

## ðŸ“„ License

This project is licensed under the **MIT License** â€” see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with â¤ï¸ for the Linux community**

*LinuxPilot AI â€” Intelligent. Safe. Fast.*

</div>

