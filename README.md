# OpenClaw USB Portable (二次创作/非原创版本) ⚡

> [!IMPORTANT]
> **声明**：本仓库是基于原作者 [techjarves/OpenClaw-USB-Portable](https://github.com/techjarves/OpenClaw-USB-Portable) 的开源项目进行的**二次创作**，并非原创。本版本进行了一些定制修改和功能优化，版权归原作者所有。

---

## 📢 最新更新与修正日志 (Update & Bugfix Logs)

### **v1.1.0-custom (2026-07-01)**
*   **更新功能 (New Features)**:
    *   **GitHub 自动更新提示**：在 Windows (`run.bat` -> `bin/windows.ps1`) 和 Linux/macOS (`run.sh` -> `bin/unix.sh`) 启动时，新增了交互式提示，用户可选择是否联网检查并更新 OpenClaw 核心程序到官方 GitHub 最新开发版。
    *   **工具菜单更新选项优化**：在工具菜单（Tools Menu）的选项 `7. Update` 中，已将原本更新至 npm 官方稳定版的命令修改为更新至 [OpenClaw 官方 GitHub 最新开发版本](https://github.com/openclaw/openclaw)。
*   **修正的 Bug (Bugfixes)**:
    *   解决了原本直接更新到 npm 稳定版而无法直接获取 GitHub 仓库最新特性的限制。

---

Run OpenClaw from a portable workspace on Windows, Linux, and macOS.

<p>
  <img alt="Windows" src="https://img.shields.io/badge/Windows-run.bat-0078D4?style=flat-square">
  <img alt="Linux" src="https://img.shields.io/badge/Linux-run.sh-FCC624?style=flat-square">
  <img alt="macOS" src="https://img.shields.io/badge/macOS-run.sh-000000?style=flat-square">
  <img alt="Portable Node" src="https://img.shields.io/badge/Node.js-portable-339933?style=flat-square">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue?style=flat-square">
</p>

OpenClaw USB Portable is a launcher project for people who want the same OpenClaw workspace available across multiple computers without installing Node.js, npm, or OpenClaw globally on each machine.

The user-facing entrypoints are intentionally simple:

```text
run.bat   Windows
run.sh    Linux and macOS
```

Everything else is internal runtime, configuration, or portable workspace data.

## What It Does ✨

- Downloads a portable Node.js runtime into this project on first run.
- Installs OpenClaw into a project-local package folder.
- Keeps OpenClaw config, sessions, workspace files, memory, and generated state under `data/`.
- Uses one shared portable workspace across Windows, Linux, and macOS.
- Keeps generated runtime files, logs, credentials, and chat history out of Git.

This is a portable workspace, not a single universal binary. Each operating system has its own runtime because Windows, Linux, and macOS use different binaries.

## Quick Start 🚀

### Windows

Double-click:

```text
run.bat
```

Or run from PowerShell:

```powershell
.\run.bat
```

### Linux and macOS

Run:

```bash
sh run.sh
```

First run on each operating system needs internet access to download that OS runtime and install OpenClaw. After that, the same OS can reuse its portable runtime from the drive.

## Main Menu

```text
Portable OpenClaw

1. Setup / Change AI
2. Chat
3. Dashboard
4. Tools
5. Run OpenClaw Command
0. Exit
```

Use `Setup / Change AI` first to configure your model provider. After setup, use `Chat` or `Dashboard` for daily work.

`Run OpenClaw Command` is available for commands shown by OpenClaw itself, for example:

```text
openclaw pairing approve telegram R2F8ZL5S
```

## Portable Data Model

Shared state lives under `data/`:

```text
data/
  config/       OpenClaw config
  openclaw/     OpenClaw state, sessions, logs, memory, canvas data
  home/         Portable home directory used by tools
  workspace/    Files the agent works on
  temp/         Temporary files
```

Generated platform-specific files live outside `data/`:

```text
runtime/        Portable Node.js runtimes
packages/       OpenClaw installs and npm cache
logs/           Launcher and install logs
```

These folders are ignored by Git because they may contain large binaries, local logs, credentials, chat history, or machine-specific state.

## Project Layout

```text
OpenClaw-USB-Portable/
  run.bat
  run.sh
  README.md
  LICENSE
  .gitignore
  .gitattributes

  bin/
    windows.ps1
    unix.sh
    portable-env.ps1
    portable-env.sh

  templates/
    openclaw.portable.json

  data/
    .gitkeep
```

## Why `.gitattributes` Is Included

The launchers need correct line endings:

```text
*.bat  CRLF
*.ps1  CRLF
*.sh   LF
```

This keeps Windows scripts friendly on Windows and shell scripts runnable on Linux/macOS.

## What Is Not Committed

The repository intentionally excludes:

```text
runtime/
packages/
logs/
data/config/
data/openclaw/
data/home/
data/workspace/
data/temp/
```

Do not commit these folders unless you intentionally want to publish local runtime files or private workspace data.

## Typical Use Cases

- Carry the same OpenClaw workspace between laptops.
- Use OpenClaw on a clean machine without installing Node.js globally.
- Keep model setup, sessions, and workspace files together in one portable folder.
- Record demos or tutorials without relying on a machine-specific development environment.

## Notes

- First run per OS requires internet.
- The launcher uses local loopback Gateway access for local Chat and Dashboard.
- API keys, bot tokens, sessions, and generated state belong in ignored `data/` folders.