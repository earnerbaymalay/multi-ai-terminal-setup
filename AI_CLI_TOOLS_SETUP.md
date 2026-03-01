# AI CLI Tools - Complete Setup Guide

## Overview
This guide covers the setup of all AI CLI tools installed on this Windows system:
- **Claude** (Anthropic)
- **Kimi** (Moonshot AI)
- **Gemini** (Google)
- **Qwen** (Alibaba)
- **Codex** (OpenAI)
- **Kilo Code** (AI-powered code editor)
- **Ollama** (Local LLMs)

---

## API Keys & Authentication

### 1. Claude (Anthropic)
**Authentication Method**: OAuth (already configured via `claude login`)

**Verify Setup**:
```powershell
claude auth status
```

**If re-authentication needed**:
```powershell
claude login
```

---

### 2. Kimi (Moonshot AI)
**Authentication Method**: OAuth (already configured)

**Credentials stored at**: `C:\Users\pat21\.kimi\credentials\kimi-code.json`

**Verify Setup**:
```powershell
kimi /login
```

**Environment Variable (optional)**:
```powershell
[Environment]::SetEnvironmentVariable("KIMI_API_KEY", "your-api-key", "User")
```

---

### 3. Gemini (Google)
**Authentication Method**: OAuth (already configured)

**Verify Setup**:
```powershell
gemini auth status
```

**Alternative: API Key for automation**:
1. Get API key from: https://aistudio.google.com/app/apikey
2. Set environment variable:
```powershell
[Environment]::SetEnvironmentVariable("GOOGLE_API_KEY", "your-api-key", "User")
```

---

### 4. Qwen (Alibaba)
**Authentication Method**: OAuth preferred

**Setup**:
```powershell
qwen auth
```

**Alternative: API Key**:
```powershell
[Environment]::SetEnvironmentVariable("QWEN_API_KEY", "your-api-key", "User")
```

---

### 5. Codex (OpenAI)
**Authentication Method**: API Key Required

**Setup Steps**:
1. Get API key from: https://platform.openai.com/api-keys
2. Set environment variable:
```powershell
[Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "sk-your-key-here", "User")
```

**Verify Setup**:
```powershell
codex "Hello, verify my setup"
```

---

### 6. Kilo Code
**Authentication Method**: Built-in (configured on first launch)

**Launch**:
```powershell
kilo
```

**Windows Terminal shortcut**: `Ctrl+Alt+L` → opens AI: Kilo Code profile

**Verify Setup**:
```powershell
kilo --version
```

**Config location**: `C:\Users\pat21\.kilo\`

---

### 7. Ollama (Local)
**Authentication Method**: None required (local)

**Verify Setup**:
```powershell
ollama list
ollama run qwen2.5-coder "Hello"
```

**Download more models**:
```powershell
ollama pull llama3.2
ollama pull phi4
```

---

## Environment Variables Summary

Create a PowerShell profile script to auto-load these:

```powershell
# Add to $PROFILE (create if doesn't exist)
notepad $PROFILE
```

Add these lines:
```powershell
# AI CLI Tools API Keys
$env:OPENAI_API_KEY = "sk-your-openai-key"           # Required for Codex
$env:GOOGLE_API_KEY = "your-google-key"              # Optional for Gemini
$env:KIMI_API_KEY = "your-kimi-key"                  # Optional for Kimi
$env:QWEN_API_KEY = "your-qwen-key"                  # Optional for Qwen
$env:BRAVE_API_KEY = "your-brave-key"                # Optional for Brave Search MCP
$env:GITHUB_TOKEN = "ghp_your-token"                 # Optional for GitHub MCP

# Ollama Configuration
$env:OLLAMA_HOST = "localhost:11434"
$env:OLLAMA_NOHISTORY = "1"

# Tool Preferences
$env:POWERSHELL_TELEMETRY_OPTOUT = "1"
$env:DOTNET_CLI_TELEMETRY_OPTOUT = "1"
```

---

## MCP Servers Setup

### Install MCP Server Packages
```powershell
# Install global MCP servers for Claude
npm install -g @executeautomation/playwright-mcp-server
npm install -g @modelcontextprotocol/server-filesystem
npm install -g @modelcontextprotocol/server-fetch
npm install -g @modelcontextprotocol/server-memory
npm install -g @modelcontextprotocol/server-brave-search  # Optional: requires API key
```

### GitHub MCP Server
Uses GitHub CLI (already installed):
```powershell
gh auth status
# If not logged in:
gh auth login
```

### Brave Search MCP Server (Optional)
1. Get API key: https://brave.com/search/api/
2. Set environment variable (see above)
3. Enable in `C:\Users\pat21\.claude\mcp.json`:
   ```json
   "brave-search": { "disabled": false }
   ```

---

## Quick Reference

### Start Each Tool
```powershell
# Claude
claude

# Kimi
kimi

# Gemini
gemini

# Qwen
qwen

# Codex
codex

# Kilo Code
kilo

# Ollama (interactive)
ollama run qwen2.5-coder
```

### Get Help
```powershell
claude /help
kimi /help
gemini --help
qwen --help
codex --help
kilo --help
ollama --help
```

---

## Troubleshooting

### "API Key not found" Errors
1. Check environment variable is set: `[Environment]::GetEnvironmentVariable("OPENAI_API_KEY", "User")`
2. Restart your terminal
3. Check User vs Machine scope

### MCP Server Errors
```powershell
# Verify MCP servers are installed
npm list -g | findstr mcp

# Re-install if needed
npm install -g @executeautomation/playwright-mcp-server
```

### OAuth Issues
```powershell
# Clear credentials and re-authenticate
# Claude:
claude logout
claude login

# Kimi:
Remove-Item "$env:USERPROFILE\.kimi\credentials\*" -Force
kimi /login

# Gemini:
gemini auth logout
gemini login
```

---

## Security Best Practices

1. **Never commit API keys** to version control
2. **Use User scope** (not Machine) for environment variables on shared computers
3. **Rotate keys regularly** in your AI provider dashboards
4. **Use OAuth where possible** (more secure than API keys)
5. **Enable 2FA** on all AI provider accounts

---

## Configuration Files Location

| Tool | Config Location |
|------|----------------|
| Claude | `C:\Users\pat21\.claude\` |
| Kimi | `C:\Users\pat21\.kimi\` |
| Gemini | `C:\Users\pat21\.gemini\` |
| Qwen | `C:\Users\pat21\.qwen\` |
| Codex | `C:\Users\pat21\.codex\` |
| Kilo Code | `C:\Users\pat21\.kilo\` |
| Ollama | `C:\Users\pat21\.ollama\` |

---

*Last Updated: 2026-02-28*
