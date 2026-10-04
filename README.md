# LinuxPilot AI

**A local, safety-first AI-powered Linux operations assistant and intelligent system copilot.**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Ollama](https://img.shields.io/badge/Qwen-2.5:7B-FF6B6B?style=flat-square)](https://ollama.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-55%20passed-brightgreen?style=flat-square&logo=pytest)](tests/)

---

> LinuxPilot AI is not a generic chat wrapper around a shell. It is an **intelligent, safety-first Linux operations agent** -- a deterministic pipeline that classifies user intent, generates execution plans, collects real-time system metrics, validates commands through a **3-tier safety layer**, and synthesizes structured, actionable responses in milliseconds.

---

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Key Features](#key-features)
- [Performance & Benchmarks](#performance--benchmarks)
- [3-Tier Command Safety Layer](#3-tier-command-safety-layer)
- [Quick Start for Linux](#quick-start-for-linux)
- [Windows Development & Testing](#windows-development--testing)
- [Project Directory Structure](#project-directory-structure)
- [API Reference](#api-reference)
- [Running Tests](#running-tests)
- [Docker Support](#docker-support)
- [Environment Configuration](#environment-configuration)
- [Demo Queries](#demo-queries)
- [Tech Stack](#tech-stack)
- [Contributing](#contributing)
- [License](#license)

---

## Architecture Overview

Conventional terminal AI tools send raw prompts to an LLM and run unvetted shell commands directly -- a dangerous and unpredictable approach.

LinuxPilot AI introduces a **deterministic, multi-stage safety pipeline**:

```mermaid
flowchart TD
    A[User Natural Language Query] --> B[Intent Classifier\nDeterministic Fast-Path + Qwen 2.5 Fallback]
    B --> C[Task Planner\nDeterministic & Contextual Workflows]
    C --> D[Tool Registry\npsutil | os.scandir | systemctl | journalctl]
    D --> E[3-Tier Command Safety Validator\nREAD_ONLY | MODIFYING | DANGEROUS]
    E --> F[Structured Execution & Response Synthesis]
    F --> G[React 18 + TypeScript Dashboard UI]
```

```text
Pipeline Breakdown:
1. User Query          -> Free-form text describing a task or problem.
2. Intent Classifier   -> Fast regex/heuristic matcher (sub-millisecond) with local LLM fallback.
3. Task Planner        -> Assembles deterministic tool steps and parameter bindings.
4. Tool Registry       -> Safe Python-native interfaces (psutil, os.scandir, systemctl).
5. Safety Validator    -> Enforces READ_ONLY (auto-run), MODIFYING (prompt user), or DANGEROUS (block).
6. Response Synthesizer-> Structures data into readable diagnostics, cards, and tables.
7. Frontend Dashboard  -> Real-time telemetry, terminal logs, and interactive controls.
```

---

## Key Features

| Feature | Description |
|---|---|
| **Instant Diagnostics** | Live CPU usage, per-core metrics, 1m/5m/15m load averages, RAM & swap, disk capacity, and network status. |
| **High-Speed File Discovery** | Deep filesystem search powered by `os.scandir` with file extension filtering, directory limits, and size thresholds. |
| **Systemd Service Management** | Inspect and control critical services (`nginx`, `docker`, `ssh`, `apache2`, `postgresql`, `mysql`) with automated status checks. |
| **Log Analysis** | Parameterized queries for `journalctl` and `dmesg` with priority filtering (error, warning, info). |
| **Linux Concept Tutor** | Instant explanation of file permissions (`chmod 755`), tarball commands, exit codes, and shell fundamentals. |
| **Local-Only Security** | Backend defaults to `127.0.0.1`, keeping all command validation and data processing entirely local on your machine. |
| **Modern Dashboard** | Built with React 18, TypeScript, and Tailwind CSS. Features live metric graphs, command cards, and execution history. |
| **Local LLM Fallback** | Uses local Ollama with Qwen 2.5:7B-Instruct for complex, conversational, or ambiguous queries without sending data to the cloud. |
| **Automated Test Suite** | 55 unit and integration tests covering intent detection, safety gating, planner logic, and tool execution. |

---

## Performance & Benchmarks

LinuxPilot AI uses a **Deterministic Fast-Path Engine** that resolves common operational queries instantly via local APIs and heuristics, invoking Ollama only when genuine natural-language synthesis is required.

| Query / Operation | Conventional LLM Shell | LinuxPilot AI Fast-Path | Speedup |
|---|---|---|---|
| `"Why is my computer running slowly?"` | ~45,000 ms | **506 ms** | **89x faster** |
| `"Find all large files in my home directory"` | ~164,000 ms | **73 ms** | **2,200x faster** |
| `"Find Python files larger than 50 MB"` | ~120,000 ms | **50 ms** | **2,400x faster** |
| `"Show me the status of nginx"` | ~30,000 ms | **8 ms** | **3,750x faster** |
| `"Show recent system errors"` | ~25,000 ms | **16 ms** | **1,560x faster** |
| `"Explain what chmod 755 means"` | ~15,000 ms | **1 ms** | **15,000x faster** |
| `"df -h"` (read-only execution) | ~15,000 ms | **10 ms** | **1,500x faster** |
| `"systemctl restart nginx"` (confirmation gate) | ~20,000 ms | **< 1 ms** | **20,000x faster** |
| `"rm -rf /"` (blocked by safety engine) | ~10,000 ms | **2 ms** | **5,000x faster** |

---

## 3-Tier Command Safety Layer

Safety is the core architectural guarantee of LinuxPilot AI. Every shell command passes through a strict 3-tier validation rule set before execution is permitted:

```text
                         [ User Request or Agent Command ]
                                        |
                          [ Command Validation Layer ]
                                        |
      +---------------------------------+---------------------------------+
      |                                 |                                 |
      v                                 v                                 v
[ READ_ONLY ]                    [ MODIFYING ]                     [ DANGEROUS ]
Non-destructive read commands    State-altering operations         Destructive commands
(df, free, ps, top, ls,          (systemctl restart, apt           (rm -rf /, mkfs, dd,
uptime, systemctl status)        install, chmod, chown)            fork bombs, curl | bash)
      |                                 |                                 |
      v                                 v                                 v
 AUTO-EXECUTE                     EXPLICIT CONFIRMATION             PERMANENTLY BLOCKED
 Instant output                   User prompt required              Zero exceptions
```

> **Safety Guarantee:** Catastrophic commands (`rm -rf /`, raw disk writes with `dd`, fork bombs, or unvetted shell pipes) are blocked **unconditionally**. Passing `confirmed=true` will **never** bypass a blocked verdict.

---

## Quick Start for Linux

### Prerequisites

- **Linux Distribution**: Ubuntu 20.04+, Debian 11+, Fedora 38+, Linux Mint, or Arch Linux
- **Python**: 3.10+ (with `python3-venv`)
- **Node.js**: 18+ and `npm`
- **Git**
- **Ollama** (optional, for local LLM fallback): [https://ollama.ai](https://ollama.ai) with `qwen2.5:7b-instruct`

### 1. Clone the Repository

```bash
git clone https://github.com/divyamsingh21/LinuxPilot-Ai.git
cd LinuxPilot-Ai
```

### 2. Run the Automated Installer

The installer configures the Python virtual environment, installs backend dependencies, builds frontend packages, and initializes the local database.

```bash
chmod +x scripts/install.sh
./scripts/install.sh
```

### 3. Configure the Environment

```bash
cp .env.example .env
# Edit .env if you wish to adjust Ollama settings, ports, or allowed services
```

### 4. Start LinuxPilot AI

```bash
./scripts/start.sh
```

Once started, the following services will be available:

| Service | Address |
|---|---|
| **Dashboard UI** | [http://localhost:1420](http://localhost:1420) |
| **Backend API** | [http://127.0.0.1:8000](http://127.0.0.1:8000) |
| **Interactive Swagger Docs** | [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) |

### 5. Service Management

```bash
# Check service health and PID status
./scripts/status.sh

# Stop all background services cleanly
./scripts/stop.sh
```

---

## Windows Development & Testing

LinuxPilot AI supports Windows for frontend dashboard development and backend testing. Linux-native operations (`systemctl`, `journalctl`) return structured mock or status responses when running on Windows.

### Terminal 1: Backend

```powershell
# Create and activate virtual environment
python -m venv .venv
.venv\Scripts\Activate.ps1

# Install requirements
pip install -r backend/requirements.txt

# Start the FastAPI server
uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```

### Terminal 2: Frontend

```powershell
cd frontend
npm install
npm run dev
```

---

## Project Directory Structure

```text
LinuxPilot-Ai/
|-- backend/                    # FastAPI backend
|   |-- agent/                  # Orchestrator and task planner
|   |-- ai/                     # Intent classifier, Ollama client, prompt templates
|   |-- api/                    # REST route endpoints (agent, diagnostics, logs, search)
|   |-- commands/               # Command execution and safe subprocess runner
|   |-- database/               # SQLite database models and session helpers
|   |-- diagnostics/            # CPU, memory, disk, and network collectors
|   |-- search/                 # Filesystem search engine (os.scandir)
|   |-- services/               # Systemd service manager
|   |-- utils/                  # Logger, configuration, and helpers
|   |-- validator/              # 3-tier command safety engine
|   \-- main.py                 # FastAPI application entry point
|-- frontend/                   # React 18 + TypeScript + Vite + Tailwind CSS
|   |-- src/
|   |   |-- components/         # UI components (dashboard, metrics, chat, logs)
|   |   |-- hooks/              # Custom React hooks
|   |   \-- services/           # Backend API communication clients
|   \-- src-tauri/              # Optional Tauri desktop shell
|-- tests/                      # Pytest automated test suite (55 tests)
|-- scripts/                    # install.sh, start.sh, stop.sh, status.sh
|-- docker/                     # Dockerfiles for containerized environments
|-- docker-compose.yml          # Container configuration
|-- requirements.txt            # Python dependencies
\-- .env.example                # Environment configuration template
```

---

## API Reference

| Endpoint | Method | Description |
|---|---|---|
| `/api/health` | `GET` | Health check and active configuration status |
| `/api/agent/ask` | `POST` | Primary agent endpoint: classify -> plan -> execute -> synthesize |
| `/api/agent/history` | `GET` | Retrieve recent interaction history from SQLite |
| `/api/intent/classify` | `POST` | Run intent classification and parameter extraction |
| `/api/diagnostics/cpu` | `GET` | Real-time CPU usage, per-core stats, and load averages |
| `/api/diagnostics/memory` | `GET` | Total, available, and used RAM plus swap space |
| `/api/diagnostics/disk` | `GET` | Mount points, total storage, used percentage |
| `/api/diagnostics/network` | `GET` | Default gateway, IP addresses, DNS, and connection test |
| `/api/services/{name}/status` | `GET` | Check systemd service status (e.g. nginx, docker) |
| `/api/services/{name}/restart`| `POST`| Restart a service (triggers confirmation check) |
| `/api/logs/journalctl` | `POST` | Query system logs with safety-checked parameters |
| `/api/logs/dmesg` | `POST` | Inspect kernel ring buffer logs safely |
| `/api/search/files` | `POST` | Search files by name pattern, size threshold, and path |
| `/api/execute/command` | `POST` | Validate and execute a shell command through safety checks |

Interactive API documentation and schema testing are available at `http://127.0.0.1:8000/docs`.

---

## Running Tests

LinuxPilot AI includes a comprehensive test suite covering all critical modules:

```bash
# Run the complete test suite
python -m pytest -v
```

### Test Suite Summary

```text
tests/test_api.py                 (9 tests)   PASSED
tests/test_command_safety.py      (4 tests)   PASSED
tests/test_command_validator.py  (13 tests)   PASSED
tests/test_intent_classifier.py   (7 tests)   PASSED
tests/test_orchestrator.py        (9 tests)   PASSED
tests/test_planner.py             (6 tests)   PASSED
tests/test_tools.py               (7 tests)   PASSED
============================= 55 passed in ~3s =============================
```

---

## Docker Support

Run LinuxPilot AI in an isolated container environment using Docker Compose:

```bash
# Build and run the complete stack
docker-compose up --build

# Run only the backend service
docker-compose up backend
```

---

## Environment Configuration

Copy `.env.example` to create your local `.env` file:

```ini
# AI / Ollama Configuration
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=qwen2.5:7b-instruct

# Application Settings
APP_ENV=development
LOG_LEVEL=INFO
API_HOST=127.0.0.1
API_PORT=8000

# Database
DATABASE_URL=sqlite:///./linuxpilot.db

# Command Execution Safety Settings
ALLOW_COMMAND_EXECUTION=false
ALLOWED_SERVICES=docker,apache2,nginx,ssh,mysql,postgresql
COMMAND_TIMEOUT_SECONDS=20
```

> **Security Note:** Keep `ALLOW_COMMAND_EXECUTION=false` during initial setup until you are ready to allow the agent to execute modifying commands on your host system.

---

## Demo Queries

Try these sample queries in the dashboard to explore LinuxPilot AI's capabilities:

1. **System Health Check**: `"Why is my computer running slowly?"`
   - *Result*: Runs instant diagnostics across CPU, RAM, and disk in under 500 ms.
2. **Find Large Files**: `"Find all large files in my home directory"`
   - *Result*: Scans your home directory and returns files over 100 MB in ~70 ms.
3. **Targeted Search**: `"Find Python files larger than 50 MB"`
   - *Result*: Extracts file type and size parameters and returns matching files.
4. **Service Control**: `"Restart nginx"`
   - *Result*: Triggers the user confirmation gate before taking any modifying action.
5. **Safety Block Demo**: `"rm -rf /"`
   - *Result*: Instantly intercepted and permanently blocked with a clear warning.
6. **Concept Explanation**: `"Explain what chmod 755 means"`
   - *Result*: Provides a clear, detailed breakdown of user, group, and other permissions.

---

## Tech Stack

| Category | Technologies |
|---|---|
| **Backend** | Python 3.10+, FastAPI 0.115, Uvicorn, Pydantic v2 |
| **AI & LLM** | Ollama, Qwen 2.5:7B-Instruct (local execution) |
| **System Diagnostics** | psutil, os.scandir, systemctl, journalctl, dmesg |
| **Frontend UI** | React 18, TypeScript, Vite, Tailwind CSS |
| **Desktop Integration** | Tauri (optional desktop app build) |
| **Database** | SQLite (conversation and execution history) |
| **Testing** | Pytest, pytest-asyncio (55 automated tests) |
| **Deployment** | Shell scripts (`scripts/`), Docker, Docker Compose |

---

## Contributing

Contributions and feedback are welcome! To contribute:

1. Fork the repository on GitHub.
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "feat: add my new feature"`
4. Push to your branch: `git push origin feature/my-feature`
5. Ensure all tests pass: `python -m pytest -v`
6. Open a Pull Request.

---

## License

This project is licensed under the [MIT License](LICENSE).
