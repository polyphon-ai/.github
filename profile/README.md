<div align="center">

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="media/wordmark-light.svg">
  <source media="(prefers-color-scheme: light)" srcset="media/wordmark-dark.svg">
  <img src="media/wordmark-dark.svg" alt="Polyphon" height="60">
</picture>

<br><br>

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/polyphon-ai/polyphon/blob/main/LICENSE) [![Follow on X](https://img.shields.io/badge/Follow-%40PolyphonAI-000?logo=x&logoColor=white)](https://x.com/intent/follow?screen_name=PolyphonAI) [![GitHub Sponsors](https://img.shields.io/github/sponsors/coreydaley?logo=githubsponsors&logoColor=white&color=EA4AAA)](https://github.com/sponsors/coreydaley)

<br>

**One chat. Many voices.**

Polyphon is a free, open source desktop app for orchestrating conversations between multiple AI models simultaneously. You send a message — every voice in the session responds, reads each other's replies, and builds on what came before.

*A critic and a builder. A cloud model and a local one. Running together, in the same conversation.*

<br>

<img src="media/screenshot.png" width="840" alt="Polyphon screenshot" />

<br>

</div>

---

<h3 align="center">All your voices, in one conversation</h3>

| 🔑 API | 💻 CLI | 🏠 Local / custom |
|:---:|:---:|:---:|
| Anthropic Claude · OpenAI GPT · Google Gemini | Claude Code · Codex · GitHub Copilot | Ollama · LM Studio · any OpenAI-compatible endpoint |

---

<h3 align="center">Your data. Your machine. Your rules.</h3>

| 🔒 Local-first | 🚫 No telemetry | 👤 No account |
|:---:|:---:|:---:|
| Sessions and compositions live on your machine, encrypted at rest | Never phones home — no usage data, no analytics, no exceptions | No sign-up required. No usage cap from us — you pay your API providers directly |

API keys are read from your shell environment and never leave the main process. These aren't marketing claims. The source is here.

---

<h3 align="center">Built for developers</h3>

| 🔌 SDK & TCP API | 🤖 MCP Server |
|:---:|:---:|
| A built-in JSON-RPC 2.0 API server lets you control Polyphon programmatically. The [`@polyphon-ai/js`](https://github.com/polyphon-ai/polyphon-js) SDK and `poly` CLI let you create sessions, run prompts, and stream responses from any script or CI pipeline. | Use Polyphon as a tool inside your agent workflows. Claude Code, Cursor, Codex CLI, and GitHub Copilot can list compositions, create sessions, and broadcast questions to your full ensemble — synchronously, over stdio. |

---

### Repositories

| Repo | Description |
|---|---|
| **[polyphon](https://github.com/polyphon-ai/polyphon)** | Core Electron desktop app — TypeScript, React, SQLCipher |
| **[obsidian-polyphon](https://github.com/polyphon-ai/obsidian-polyphon)** | Obsidian plugin — multi-voice AI conversations inside your vault |
| **[vscode-polyphon](https://github.com/polyphon-ai/vscode-polyphon)** | VS Code extension — multi-voice AI conversations with code context awareness |
| **[polyphon-js](https://github.com/polyphon-ai/polyphon-js)** | JavaScript/TypeScript SDK — connect to Polyphon from your own code |
| **[polyphon-ai.github.io](https://github.com/polyphon-ai/polyphon-ai.github.io)** | Source for [polyphon.ai](https://polyphon.ai) — Hugo site with docs and blog |

---

### Get started

- **[Download Polyphon](https://polyphon.ai/#download)** — macOS, free
- **[Documentation](https://polyphon.ai/docs/)** — installation, providers, sessions
- **[Roadmap](https://polyphon.ai/roadmap/)** — what's shipped and what's coming

### Get involved

- **[Join a discussion](https://github.com/polyphon-ai/.github/discussions)** — questions, ideas, show and tell
- **[GitHub Sponsors](https://github.com/sponsors/coreydaley)** — support development directly
