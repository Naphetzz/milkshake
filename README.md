# Milkshake

AI-powered Roblox Studio coding assistant. Generate Luau scripts with multiple AI providers, auto-sync code directly to the correct Studio location, and manage your project with full instance tree awareness.

![Electron](https://img.shields.io/badge/Electron-28-blue)
![React](https://img.shields.io/badge/React-18-61dafb)
![License](https://img.shields.io/badge/License-MIT-green)

## Features

- **Multi-Provider AI** — OpenAI, DeepSeek, Gemini, Groq, Anthropic, Mistral, OpenRouter, Together AI, Ollama (local)
- **MCP Integration** — Model Context Protocol server with 13 tools for full Studio awareness
- **Auto-Sync** — Code is placed in the correct service (ServerScriptService, StarterGui, ReplicatedStorage, etc.) automatically
- **Instance Tree Browser** — View your Roblox project structure in real-time
- **Thinking Mode** — Low / Medium / Max temperature control
- **Prompt Templates** — 10 built-in templates for combat, UI, economy, gameplay, backend + custom templates
- **Code History** — Browse and restore previous generations
- **Dev Mode** — Password-protected API key for team sharing
- **Cross-Platform** — Windows (.exe), Linux (.AppImage), macOS (.dmg)

## Quick Start

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [Roblox Studio](https://www.roblox.com/create) with the Milkshake plugin installed

### Install & Run

```bash
git clone https://github.com/yourname/milkshake.git
cd milkshake
npm install
npm start
```

## Setup

### 1. Get an API Key

Get a key from any supported provider:

| Provider | URL | Free Tier |
|----------|-----|-----------|
| DeepSeek | [platform.deepseek.com](https://platform.deepseek.com) | Yes |
| OpenAI | [platform.openai.com](https://platform.openai.com) | No |
| Google Gemini | [aistudio.google.com](https://aistudio.google.com) | Yes |
| Groq | [console.groq.com](https://console.groq.com) | Yes |
| Anthropic | [console.anthropic.com](https://console.anthropic.com) | No |
| Ollama | [ollama.ai](https://ollama.ai) | Free (local) |

### 2. Configure in Milkshake

1. Open **Settings** (sidebar or press `6`)
2. Paste your API key under the provider
3. Select the provider and model in the Chat panel

### 3. Install the Roblox Plugin

1. Open Roblox Studio
2. Go to **Plugins** → **Manage Plugins** → **Browse Local Files**
3. Navigate to `Plugins/Milkshake/`
4. Place `Milkshake.lua` from `src/plugin/` into that folder
5. Restart Studio — the Milkshake plugin appears in the toolbar

### 4. Connect

1. Click the **Milkshake** plugin button in Studio
2. The status indicator in the title bar turns green when connected
3. Start generating — code auto-syncs to the right location

## Usage

### Chat

Type what you want to build in natural language. Examples:

- "Create a damage system with critical hits"
- "Build a inventory UI with drag and drop"
- "Make a DataStore save system"
- "Add a round-based game mode"

### Thinking Mode

| Mode | Temp | Best for |
|------|------|----------|
| Low | 0.3 | Precise, deterministic code |
| Medium | 0.7 | General purpose (default) |
| Max | 1.0 | Creative, experimental |

### MCP Tools

When connected to Studio, Milkshake has access to these tools:

| Tool | Description |
|------|-------------|
| `get_project_tree` | Full instance hierarchy |
| `get_service_contents` | Contents of a specific service |
| `find_instance` | Search by name or class |
| `get_instance_properties` | Read properties of any instance |
| `sync_code` | Push Luau to the correct location |
| `create_instance` | Add new instances to the tree |
| `delete_instance` | Remove instances |
| `rename_instance` | Rename instances |
| `modify_property` | Change instance properties |
| `execute_code` | Run code in Studio command bar |
| `get_selection` | Read current Studio selection |
| `set_selection` | Change Studio selection |
| `get_script_source` | Read source of a script |

## Dev Mode

For teams: store a shared API key with password protection.

1. Create a `.env` file in the project root:
   ```
   MILKSHAKE_DEV_KEY=sk-your-key
   MILKSHAKE_DEV_PASSWORD=your-password
   MILKSHAKE_DEV_PROVIDER=deepseek
   MILKSHAKE_DEV_MODEL=deepseek-v4-flash
   ```
2. In Settings → **Dev Mode**, enter the password to unlock
3. Provider/model are auto-configured and locked to the dev key

## CI/CD

GitHub Actions workflow included (`.github/workflows/build.yml`). Push a tag to trigger builds for all platforms:

```bash
git tag v1.0.0
git push --tags
```

Artifacts: `.exe` (NSIS installer + portable), `.AppImage`, `.deb`, `.rpm`, `.dmg`

## Project Structure

```
milkshake/
├── src/
│   ├── main/                  # Electron main process
│   │   ├── main.js            # App entry, IPC handlers
│   │   ├── preload.js         # Context bridge
│   │   ├── ai-providers.js    # 9 AI provider backends
│   │   ├── mcp-server.js      # MCP server with 13 tools
│   │   ├── websocket-server.js # Studio connection (WS + HTTP)
│   │   ├── project-manager.js # Project CRUD + history
│   │   └── prompt-templates.js # Built-in + custom templates
│   ├── renderer/              # React frontend
│   │   ├── components/
│   │   │   ├── ChatPanel.jsx      # Chat interface
│   │   │   ├── CodeViewer.jsx     # Syntax-highlighted output
│   │   │   ├── Dropdown.jsx       # Custom dropdown (keyboard nav)
│   │   │   ├── Icons.jsx          # SVG icon library
│   │   │   ├── Settings.jsx       # API keys + dev mode
│   │   │   ├── Sidebar.jsx        # Navigation
│   │   │   ├── TitleBar.jsx       # Custom title bar
│   │   │   ├── InstanceTree.jsx   # Project tree viewer
│   │   │   ├── ProjectManager.jsx # Project management
│   │   │   ├── TemplateBrowser.jsx # Prompt templates
│   │   │   ├── Marketplace.jsx    # Plugin marketplace
│   │   │   └── DiffView.jsx       # Code diff viewer
│   │   └── styles/
│   │       └── main.css           # Catppuccin dark theme
│   └── plugin/
│       └── Milkshake.lua          # Roblox Studio plugin
├── build/                     # App icons
├── .github/workflows/         # CI/CD
├── .env.example               # Environment template
└── package.json
```

## Tech Stack

- **Electron 28** — Desktop shell
- **React 18** — UI framework
- **Vite 5** — Build tool
- **electron-store** — Persistent settings
- **highlight.js** — Luau syntax highlighting
- **Catppuccin Mocha** — Color palette

## License

MIT
