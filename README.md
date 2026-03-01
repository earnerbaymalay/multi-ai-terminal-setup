# 🤖 Multi-AI Terminal Setup

> **A complete Windows Terminal configuration for running Claude, Kimi, Gemini, Qwen, Codex, Kilo Code, and Ollama — each with a dedicated profile, colour scheme, keyboard shortcut, and branded welcome screen.**

![Windows Terminal](https://img.shields.io/badge/Windows%20Terminal-1.x%2B-blue?style=flat-square)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue?style=flat-square)
![AI Tools](https://img.shields.io/badge/AI%20Tools-7-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-orange?style=flat-square)

---

## 🎯 What This Sets Up

A single `settings.json` that transforms Windows Terminal into a purpose-built AI command centre:

- **8 named profiles** — one per AI tool, plus PowerShell default and AI Compare mode
- **8 custom colour schemes** — each AI has its own branded palette
- **Keyboard shortcuts** — open any AI in a new tab instantly
- **Branded welcome boxes** — each profile greets you with commands and shortcuts
- **AI quick-reference bar** — shown in every PowerShell session on startup
- **Environment variables** — `AI_CONTEXT` and `AI_HUB_DIR` visible to all AI tools

---

## 🤖 AI Tools Roster

| Tool | Key | Shortcut | Colour | CLI Command |
|------|-----|----------|--------|-------------|
| 🟠 Claude | `c` | `Ctrl+Alt+C` | Gold/Amber | `claude` |
| 🌙 Kimi | `k` | `Ctrl+Alt+K` | Steel Blue | `kimi` |
| ♊ Gemini | `g` | `Ctrl+Alt+G` | Emerald | `gemini` |
| 🌸 Qwen | `q` | `Ctrl+Alt+Q` | Hot Pink | `qwen` |
| ⌨️ Codex | `cx` | `Ctrl+Alt+X` | Teal | `codex` |
| ▲ Kilo Code | `kc` | `Ctrl+Alt+L` | Pink/Purple | `kilo` |
| 🦙 Ollama | `o` | `Ctrl+Alt+O` | Grey | `ollama` |
| 🔬 AI Compare | — | `Ctrl+Alt+A` | Yellow | (split pane) |

---

## 🚀 Install

### Step 1 — Prerequisites

- [Windows Terminal](https://aka.ms/terminal) installed (or from Microsoft Store)
- Each AI CLI tool installed and on your `PATH`
- PowerShell 5.1 or 7+

### Step 2 — Apply the settings

```powershell
# Backup your current settings first
$dst = "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState"
Copy-Item "$dst\settings.json" "$dst\settings.json.bak"

# Apply the new config
Copy-Item windows-terminal-settings.json "$dst\settings.json"
```

Windows Terminal hot-reloads — changes apply immediately, no restart needed.

### Step 3 — Set environment variables

```powershell
# Set so all AI tools can read your context file and workspace root
[Environment]::SetEnvironmentVariable("AI_CONTEXT", "C:\Users\pat21\AI_Central\AI_CONTEXT.md", "User")
[Environment]::SetEnvironmentVariable("AI_HUB_DIR", "C:\Users\pat21\AI_Central", "User")
```

---

## 🎨 Colour Schemes

Each AI tool gets its own full colour scheme applied to its terminal tab:

| Scheme | Background | Foreground | Accent |
|--------|-----------|------------|--------|
| AI Command Hub | `#0D0D15` | `#00FFFF` | Cyan |
| AI Claude | `#0D0D15` | `#FFD700` | Gold |
| AI Kimi | `#0A0A1A` | `#87CEEB` | Steel Blue |
| AI Gemini | `#0D1F0D` | `#00FF7F` | Emerald |
| AI Qwen | `#1A0A1A` | `#FF69B4` | Hot Pink |
| AI Codex | `#0A1A1A` | `#00FFFF` | Teal |
| **AI Kilo** | `#0D0A14` | `#F472B6` | Pink/Purple |
| AI Ollama | `#0F0F0F` | `#C0C0C0` | Grey |

---

## ⌨️ All Keyboard Shortcuts

| Action | Shortcut |
|--------|---------|
| New tab: Claude | `Ctrl+Alt+C` |
| New tab: Kimi | `Ctrl+Alt+K` |
| New tab: Gemini | `Ctrl+Alt+G` |
| New tab: Qwen | `Ctrl+Alt+Q` |
| New tab: Codex | `Ctrl+Alt+X` |
| New tab: Kilo Code | `Ctrl+Alt+L` |
| New tab: Ollama | `Ctrl+Alt+O` |
| New tab: AI Compare | `Ctrl+Alt+A` |
| New window | `Ctrl+Alt+N` |
| Split pane (duplicate) | `Alt+Shift+D` |
| Close pane | `Ctrl+W` |
| Focus left/right/up/down | `Alt+Arrow` |
| Full screen | `F11` |
| Focus mode | `Ctrl+Alt+F` |
| Command palette | `Ctrl+Shift+P` |

---

## 📋 Welcome Box Format

Every AI profile shows a branded box on open:

```
╔════════════════════════════════════════════════════════════════╗
║              ▲ KILO CODE - AI POWERED EDITOR                   ║
╠════════════════════════════════════════════════════════════════╣
║  Commands: kilo, kilo <file>, kilo --new-task "<prompt>"       ║
║  Shortcut:  Ctrl+Alt+L                                         ║
╚════════════════════════════════════════════════════════════════╝
```

Plus the shared startup header and quick-reference bar showing all AI aliases.

---

## 🔧 PowerShell Profile

The `AI_CLI_TOOLS_SETUP.md` documents the PowerShell profile (`$PROFILE`) that:

- Displays the system info header on every new tab
- Shows the AI quick-reference box with all shortcuts
- Defines shorthand functions (`c`, `k`, `g`, `q`, `cx`, `kc`, `o`)
- Exposes `ai-help`, `ai-status`, `ai-compare`, `sysinfo`, `diskinfo`

---

## 🌐 Routing Config

`routing.conf` documents which AI is preferred for which task type:

```
code_generation  → kilo, claude, codex
analysis         → claude, gemini
creative         → claude, kimi
local_only       → ollama
fast_iteration   → kilo, codex
```

---

## 📁 Files

```
multi-ai-terminal-setup/
├── windows-terminal-settings.json   ← Drop-in WT config
├── AI_CONTEXT.md                    ← Shared AI context (loaded via AI_CONTEXT env var)
├── CLAUDE.md                        ← Claude-specific directives
├── GEMINI.md                        ← Gemini-specific directives
├── routing.conf                     ← AI task routing preferences
├── AI_CLI_TOOLS_SETUP.md            ← PowerShell profile setup guide
└── README.md
```

---

## ❓ FAQ

**Do I need all 7 AI tools installed?**
No — profiles for missing tools will just show an error when you try to open them. All other profiles work fine.

**Can I change the starting directory?**
Yes — edit `"startingDirectory"` in each profile in `windows-terminal-settings.json`.

**The welcome box shows an error about the AI CLI not being found.**
The profile runs `claude --help | Out-Null` on startup to check. If the tool isn't installed, suppress the error by removing that line from the profile's `"commandline"`.

---

## 🤝 Contributing

PRs welcome for new AI tool profiles. Follow the existing pattern: profile entry + colour scheme + keybinding + welcome box.

---

## 📄 License

MIT — use freely, adapt to your tools.
