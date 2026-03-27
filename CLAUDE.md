# polyphon-ai — CLAUDE.md

This directory contains the related repositories for the Polyphon project. Each has its own `CLAUDE.md` with project-specific details. This file describes how the projects relate to each other.

## Projects

| Repository | Purpose | Stack |
|---|---|---|
| [`polyphon/`](./polyphon/) | Core Electron desktop app | TypeScript, React 19, Electron 41, SQLCipher |
| [`polyphon-js/`](./polyphon-js/) | JavaScript/TypeScript SDK | TypeScript, Node.js, published as `@polyphon-ai/js` |
| [`obsidian-polyphon/`](./obsidian-polyphon/) | Obsidian plugin client | TypeScript, Obsidian Plugin API |
| [`vscode-polyphon/`](./vscode-polyphon/) | VS Code extension | TypeScript, VS Code Extension API |
| [`polyphon-ai.github.io/`](./polyphon-ai.github.io/) | Marketing and docs website | Hugo, deployed to polyphon.ai |

## How They Interact

### polyphon → polyphon-js (SDK sync)

`polyphon` is the **complete source of truth** for everything in `polyphon-js/src/`. On each Polyphon release, the `sync-sdk.yml` workflow copies all SDK files to `polyphon-js`, bumps the SDK version to match, and publishes `@polyphon-ai/js` to npm.

| polyphon source | polyphon-js destination |
|---|---|
| `src/shared/types.ts`, `src/shared/api.ts` | `src/types.ts`, `src/api.ts` |
| `src/sdk/client.ts`, `errors.ts`, `token.ts`, `index.ts` | `src/client.ts`, etc. |
| `src/sdk/testing/` | `src/testing/` |
| `src/sdk/**/*.test.ts` | `src/**/*.test.ts` |

SDK tests run in polyphon CI first (against the real server implementation) before syncing, ensuring correctness before each publish.

### polyphon ↔ obsidian-polyphon / vscode-polyphon (API contract)

`polyphon` exposes a **JSON-RPC 2.0 TCP API** on port 7432 (default). Both the Obsidian plugin and VS Code extension connect to this socket and call methods to authenticate, list compositions, manage sessions, and stream voice responses.

Both clients import types directly from `@polyphon-ai/js`, keeping them in sync with the SDK automatically. Sessions created by each client are tagged with a `source` field (`"obsidian"` or `"vscode"`) so each client only surfaces its own sessions in its UI.

Key API methods:

| Method | Purpose |
|---|---|
| `api.authenticate` | Auth with token from `~/Library/Application Support/Polyphon/api.key` |
| `compositions.list` / `compositions.get` | Fetch compositions |
| `sessions.list` / `sessions.create` / `sessions.get` | Manage sessions |
| `sessions.messages` / `sessions.rename` / `sessions.export` | Session operations |
| `voice.broadcast` | Send a message; streams `stream.chunk` notifications back |
| `settings.getUserProfile` | Fetch conductor profile |

### polyphon → polyphon-ai.github.io (release workflow)

On each Polyphon release, the `update-download-version.yml` GitHub Actions workflow in `polyphon`:
1. Checks out `polyphon-ai.github.io`
2. Updates `params.downloadVersion` in `hugo.yaml`
3. Creates a release blog post in `content/blog/`
4. Commits, pushes, and triggers a site deploy

Direct site edits (docs, roadmap, theme changes) are committed to `polyphon-ai.github.io` independently.

### polyphon-ai.github.io → polyphon/obsidian-polyphon/vscode-polyphon (documentation)

The site hosts all user-facing documentation for all client projects:
- `content/docs/polyphon/` — main app docs
- `content/docs/integrations/obsidian-polyphon/` — Obsidian plugin docs
- `content/docs/integrations/vscode-polyphon/` — VS Code extension docs
- `content/docs/for-developers/api.md` — full JSON-RPC API reference
- `content/docs/for-developers/mcp.md` — MCP server docs

When API contracts or features change in any project, update the relevant docs here.

## Cross-Project Workflows

### Adding a new API method to polyphon
1. Implement in `polyphon/src/main/api/`
2. Add types to `polyphon/src/shared/api.ts`
3. Update `MockPolyphonServer` in `polyphon/src/sdk/testing/MockPolyphonServer.ts` to handle the new method
4. Add tests in `polyphon/src/sdk/client.test.ts`
5. On release, `sync-sdk.yml` automatically syncs everything to `polyphon-js` and publishes
6. Update `polyphon-ai.github.io/content/docs/for-developers/api.md`

### Releasing a new version
1. Bump version in `polyphon` with `make bump-version VERSION=x.y.z`
2. Run `release.yml` — signs, notarizes, and publishes the macOS DMG
3. Run `update-download-version.yml` — updates the site and creates the release blog post

### Updating client documentation
- App docs: `polyphon-ai.github.io/content/docs/polyphon/`
- Obsidian plugin docs: `polyphon-ai.github.io/content/docs/integrations/obsidian-polyphon/`
- VS Code extension docs: `polyphon-ai.github.io/content/docs/integrations/vscode-polyphon/`
- API reference: `polyphon-ai.github.io/content/docs/for-developers/api.md`

## Default Ports

| Service | Port |
|---|---|
| Polyphon JSON-RPC TCP API | 7432 |
