# Claudian OpenCode

> Embed [OpenCode](https://github.com/opencode-ai/opencode) into Obsidian, turning your vault into an AI coding agent's working directory.

**English** | [中文](README.md)

---

## Overview

**Claudian OpenCode** is an Obsidian desktop plugin that integrates an AI coding agent (OpenCode) directly into your Obsidian vault. Your vault becomes the agent's working directory, enabling file edits, search, shell commands, and multi-step workflows.

Optional support for [Codex](https://github.com/openai/codex) as an alternative AI provider.

## Features

- **AI Chat Panel** — Conversational interface with the AI agent inside Obsidian
- **Multi-tab Sessions** — Manage multiple independent conversations simultaneously
- **Tool Call Visualization** — Watch AI execute file edits, shell commands, and more in real time
- **Thinking Block Display** — Expand/collapse AI reasoning steps
- **File Context Management** — Attach notes as context to conversations
- **Image Attachments** — Attach and preview images within conversations
- **Status Panel** — Real-time view of todos and bash output
- **Conversation History** — Save, restore, and manage historical sessions
- **Inline Editing** — Request AI edits on selected text directly in the editor
- **BangBash Mode** — Type `!` in the input to execute shell commands directly
- **MCP Servers** — Configure and manage MCP tool servers
- **Environment Variable Management** — Manage API keys and other environment config
- **Multi-provider Support** — OpenCode as primary, Codex as optional provider
- **i18n** — Multi-language UI support

## Installation

### Via BRAT (Recommended)

1. Install [BRAT](https://obsidian.md/plugins?id=obsidian42-brat) plugin
2. Add `yudu-steven/Codian` in BRAT settings
3. Enable `Claudian OpenCode` plugin

### Manual Installation

1. Download `main.js`, `manifest.json`, and `styles.css` from [Releases](https://github.com/yudu-steven/Codian/releases)
2. Copy them to `<vault>/.obsidian/plugins/claudian/`
3. Enable the plugin in Obsidian settings

## Prerequisites

- **OpenCode**: Requires [OpenCode CLI](https://github.com/opencode-ai/opencode) installed
- **Node.js**: OpenCode depends on the Node.js runtime

## Configuration

Navigate to **Claudian OpenCode** in Obsidian settings:

### Basic Settings

| Setting | Description |
|---------|-------------|
| Provider | AI provider (OpenCode / Codex) |
| Model | AI model selection |
| Permission Mode | `yolo` (auto-execute) / `normal` (require confirmation) |
| Thinking Budget | Control AI reasoning depth |
| Effort Level | Control AI execution intensity |

### Environment Variables

Configure API keys in the **Environment Variables** section:

```bash
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
OPENCODE_SERVER_PASSWORD=your-password
```

> **Security note**: Sensitive values (API keys, passwords) stored in `.claudian/claudian-settings.json` are encrypted with AES-256-GCM. The encryption key is derived from the vault name, so cloud-synced files remain unreadable on other machines.

### MCP Servers

Add tool servers in the **MCP Servers** section:

- **stdio**: Local commands (e.g., `docker exec -i mcp-server python -m src.server`)
- **SSE**: Server-Sent Events endpoint
- **HTTP**: HTTP endpoint

## Usage

### Basic Conversation

1. Click the new chat icon in the left ribbon
2. Type a message and press `Enter` to send
3. The AI will execute tools and return results

### Quick Commands

| Command | Action |
|---------|--------|
| `/new` or `/clear` | Start a new conversation |
| `!` (on empty input) | Enter BangBash Shell mode |
| `/add-dir <path>` | Add directory to context |
| `/help` | List all commands |

### Inline Editing

1. Select text in the editor
2. Click the floating edit button
3. Enter modification instructions; the AI will show a diff preview
4. Accept or reject changes with one click

### Keyboard Navigation

| Key | Function |
|-----|----------|
| `w` / `s` (default) | Scroll messages up/down |
| `i` (default) | Focus input |
| `Escape` | Exit BangBash / close modals |
| `Enter` | Send message / execute command |
| `Shift+Enter` | New line in input |

## Security

This project takes security seriously. See the [commit history](https://github.com/yudu-steven/Codian/commits/main) for details on fixed vulnerabilities.

### Security Measures

- Sensitive environment variables encrypted at rest with AES-256-GCM
- BangBash mode requires confirmation for dangerous commands
- Diff HTML output sanitized against script injection
- Image MIME type whitelist validation (SVG rejected)
- MCP server commands flagged with security warnings
- Temporary session data cleaned up after use

## Development

```bash
# Requires TypeScript source
npm install
npm run build
```

## License

[MIT](LICENSE)

## Author

- **Yishen Tu** — [GitHub](https://github.com/YishenTu)
