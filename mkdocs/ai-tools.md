AI Developer Tools
==================

## Introduction

Revel Digital provides first-class tooling for building and managing your digital signage with AI assistants. Two complementary integrations are available today:

- **[Revel Digital Gadget Skill](#revel-digital-gadget-skill-for-claude)** — a Claude AI Skill that scaffolds complete, buildable gadget projects in React, Vue, Vanilla JS, or Angular with the Revel Digital SDK pre-wired.
- **[Revel Digital MCP Server](#revel-digital-mcp-server)** — a remote [Model Context Protocol](https://modelcontextprotocol.io) server that exposes your Revel Digital account to any MCP-compatible AI client (Claude, Cursor, Windsurf, ChatGPT, VS Code Copilot, and more), letting the assistant manage devices, media, playlists, schedules, templates, and analytics on your behalf.

Together they cover both sides of the workflow: **building** custom content with the Gadget Skill, and **operating** your signage estate through the MCP Server.

---

## Revel Digital Gadget Skill for Claude

The [Revel Digital Gadget Skill](https://github.com/RevelDigital/reveldigital-gadget-skill) is a [Claude AI Skill](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills) that turns a single natural-language prompt into a fully scaffolded, buildable gadget project — framework boilerplate, SDK integration, `gadget.yaml` with sample preferences, and optional GitHub Pages deployment.

### Supported Frameworks

| Framework | Bundler | SDK Library |
|-----------|---------|-------------|
| **React** | Vite + TypeScript | `@reveldigital/client-sdk` |
| **Vue 3** | Vite + JavaScript | `@reveldigital/client-sdk` |
| **Vanilla JS** | Parcel | `@reveldigital/client-sdk` |
| **Angular** | Angular CLI | `@reveldigital/player-client` |

### What Gets Scaffolded

- Complete project with `package.json`, build tooling, and framework boilerplate
- `gadget.yaml` with sample preferences (string, bool, style, enum) including conditional `depends` visibility
- SDK integration with a demo UI showing device info, preference access, and player actions
- `build:gadget` script chaining the framework build with the [Gadgetizer](https://www.npmjs.com/package/@reveldigital/gadgetizer) CLI that produces the gadget XML
- Optional GitHub Actions workflow for automated deployment to GitHub Pages

### Installation

#### Claude.ai (Web / Desktop / Mobile)

1. Download the latest ZIP from the [Releases page](https://github.com/RevelDigital/reveldigital-gadget-skill/releases), or grab [`revel-gadget-skill.zip`](https://github.com/RevelDigital/reveldigital-gadget-skill/raw/main/revel-gadget-skill.zip) directly
2. In Claude, open **Settings → Features → Skills**
3. Click **Add Custom Skill** and upload the ZIP
4. Toggle the skill **ON**

???+ note

    Requires **Code Execution** to be enabled under **Settings → Capabilities**.

#### Claude Code (Plugin Marketplace)

The fastest way to install in Claude Code. From any Claude Code session:

```sh
/plugin marketplace add RevelDigital/reveldigital-gadget-skill
/plugin install revel-gadget@reveldigital
```

Pull updates later with:

```sh
/plugin marketplace update reveldigital
```

#### Claude Code (Manual Install)

Prefer to skip the marketplace? Copy the skill folder directly:

```sh
# Personal skills — available in every project
cp -r revel-gadget-skill ~/.claude/skills/revel-gadget

# Or project-scoped — only available in this repo
cp -r revel-gadget-skill .claude/skills/revel-gadget
```

#### Team / Enterprise Provisioning

Organization Owners can roll the skill out account-wide:

1. Go to **Organization Settings → Skills**
2. Upload the ZIP to make it available to every user in the org

### Usage

With the skill installed, just describe the gadget you want. A few examples:

> *"Create a React gadget called `weather-dashboard` for Revel Digital with GitHub Pages hosting"*

> *"Scaffold a vanilla JS Revel Digital gadget named `lobby-ticker`"*

> *"Build an Angular gadget for digital signage that shows a clock with a configurable timezone"*

Claude will prompt for any missing details (framework, name, hosting preference) and then generate the full project in your working directory. From there:

```sh
npm install
npm run build:gadget
```

The `build:gadget` script produces both the framework bundle and the gadget XML file ready for upload to Revel Digital.

### Related Resources

- **Platform docs:** [Gadget Development Guide](./gadgets.md)
- **NPM packages:**
    - [@reveldigital/client-sdk](https://www.npmjs.com/package/@reveldigital/client-sdk) — runtime SDK for React, Vue, and Vanilla JS
    - [@reveldigital/player-client](https://www.npmjs.com/package/@reveldigital/player-client) — Angular-native library with DI & RxJS
    - [@reveldigital/gadget-types](https://www.npmjs.com/package/@reveldigital/gadget-types) — TypeScript types for the OpenSocial `gadgets.Prefs` API
    - [@reveldigital/gadgetizer](https://www.npmjs.com/package/@reveldigital/gadgetizer) — CLI that generates gadget XML from `gadget.yaml`
- **Demos:** [React](https://github.com/RevelDigital/gadget-demo-react) · [Vue](https://github.com/RevelDigital/gadget-demo-vue) · [Vanilla JS](https://github.com/RevelDigital/gadget-demo-vanilla-js)

---

## Revel Digital MCP Server

The [Revel Digital MCP Server](https://reveldigital.github.io/reveldigital-mcp-cloudflare) is a hosted remote server implementing the [Model Context Protocol](https://modelcontextprotocol.io) — an open standard that lets AI assistants securely connect to external data sources and tools. Connect any MCP-compatible client and your assistant can read and write against your Revel Digital account directly: list devices, push commands, import media, build playlists, run analytics queries, and more.

There is nothing to install or host — it is a hosted service at `mcp.reveldigital.io`. All auth is handled through OAuth 2.0 against Revel Digital's identity provider, so you never paste API keys into a client config.

### Endpoints

| Transport | URL |
|-----------|-----|
| Streamable HTTP *(recommended)* | `https://mcp.reveldigital.io/mcp` |
| SSE *(legacy)* | `https://mcp.reveldigital.io/sse` |

Prefer **Streamable HTTP** for any client that supports it. SSE is provided for older MCP clients only.

### Authentication

Auth uses OAuth 2.0 / OpenID Connect via Revel Digital's identity provider (`id.reveldigital.com`). On first tool use, your client opens a browser window to sign in to your Revel Digital account and grant access. Tokens are managed and refreshed automatically by the client — no API keys required.

You'll need an existing Revel Digital account with API access.

### Client Setup

#### Claude Code (CLI)

Fastest — a single command registers the server:

```sh
claude mcp add revel-digital --transport http https://mcp.reveldigital.io/mcp
```

Or add it manually to `.mcp.json` at the root of your project:

```json
{
  "mcpServers": {
    "revel-digital": {
      "type": "url",
      "url": "https://mcp.reveldigital.io/mcp"
    }
  }
}
```

#### Claude Desktop

Edit your Claude Desktop config file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Add the following:

```json
{
  "mcpServers": {
    "revel-digital": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.reveldigital.io/mcp"
      ]
    }
  }
}
```

Save and **restart Claude Desktop**. A browser window opens for authentication the first time a tool is invoked.

???+ note

    Requires **Node.js 18+** on your machine for the `npx mcp-remote` bridge.

#### Cursor

1. Open **Settings → MCP Servers**
2. Click **Add Server**
3. Enter URL: `https://mcp.reveldigital.io/mcp`
4. Select **Streamable HTTP** as the transport
5. Save

The browser auth window opens on first tool use.

#### Windsurf

1. Open **Settings → MCP**
2. Add a remote server with URL `https://mcp.reveldigital.io/mcp`
3. Save and connect

#### VS Code (GitHub Copilot)

Add to your `settings.json`:

```json
{
  "mcp": {
    "servers": {
      "revel-digital": {
        "type": "http",
        "url": "https://mcp.reveldigital.io/mcp"
      }
    }
  }
}
```

Or, if your VS Code build only supports stdio MCP servers, use the `mcp-remote` bridge:

```json
{
  "mcp": {
    "servers": {
      "revel-digital": {
        "type": "stdio",
        "command": "npx",
        "args": [
          "mcp-remote",
          "https://mcp.reveldigital.io/mcp"
        ]
      }
    }
  }
}
```

#### ChatGPT Desktop

1. Open **Settings → Tools & Plugins → MCP Servers**
2. Click **Add Server**
3. Enter URL: `https://mcp.reveldigital.io/mcp`
4. Authenticate via the browser when prompted

#### Cloudflare AI Playground

1. Visit [playground.ai.cloudflare.com](https://playground.ai.cloudflare.com)
2. Paste `https://mcp.reveldigital.io/mcp` as the MCP server URL
3. Click **Connect** — OAuth is handled natively by the playground

### Available Tools

The server exposes **46 tools** across the following categories. Once connected, ask your assistant to list them, or just describe the task in natural language — the client will pick the right tool.

| Category | Tools | What You Can Do |
|----------|------:|-----------------|
| Account & Users | 5 | Account info, organizations, users, audit logs |
| Devices | 7 | List, create, update, delete devices; send commands; grab screenshots |
| Device Groups | 5 | Organize devices into folders |
| Media | 5 | List, get, update, delete, and import media files |
| Media Groups | 4 | Organize media into folders |
| Playlists | 5 | Create and manage content playlists |
| Playlist Groups | 2 | Organize playlists into folders |
| Schedules | 5 | Time-based content scheduling |
| Schedule Groups | 2 | Organize schedules into folders |
| Templates | 4 | Multi-zone screen layouts |
| Template Groups | 2 | Organize templates into folders |
| Data Tables | 17 | Structured data with rows, versioning, batch ops |
| Alerts | 3 | Monitor and manage device alerts |
| Analytics | 13 | Play logs, device metrics, audience data, heatmaps |

### Example Prompts

Once connected, try prompts like:

> *"List every device in my account that hasn't checked in for more than 24 hours."*

> *"Import this image URL into my Media library and add it to the `lobby-slideshow` playlist."*

> *"Show me the top 10 most-played media items across all devices last week."*

> *"Send a reboot command to every device in the `Store #42` group."*

> *"Create a new schedule that plays `holiday-promo` on all Chicago devices from Dec 20–26, 9am–9pm."*

### Debugging with MCP Inspector

To inspect raw tool responses or troubleshoot your OAuth flow, use the official [MCP Inspector](https://github.com/modelcontextprotocol/inspector):

```sh
npx @modelcontextprotocol/inspector@latest https://mcp.reveldigital.io/mcp
```

1. Open `http://localhost:5173`
2. Verify transport is **Streamable HTTP**
3. Open **OAuth Settings** and enable **Quick OAuth Flow**
4. Click **Connect** and authenticate
5. Click **List Tools** to browse and invoke tools interactively

---

## Using the Skill and MCP Together

The two integrations are designed to pair naturally:

1. Use the **Gadget Skill** in Claude Code to scaffold a custom gadget (e.g. a live sales-counter gadget pulling from a Data Table).
2. Use the **MCP Server** in the same session to populate a Data Table, create a playlist that includes the published gadget URL, and push it to a device group — all without leaving the assistant.

This tight build-and-deploy loop is the fastest way to go from idea to live content on your signage network.
