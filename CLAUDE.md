# polyphon-ai — CLAUDE.md

This directory contains three related repositories for the Polyphon project. Each has its own `CLAUDE.md` with project-specific details. This file describes how the projects relate to each other.

## Projects

| Repository | Purpose | Stack |
|---|---|---|
| [`polyphon/`](./polyphon/) | Core Electron desktop app | TypeScript, React 19, Electron 41, SQLCipher |
| [`obsidian-polyphon/`](./obsidian-polyphon/) | Obsidian plugin client | TypeScript, Obsidian Plugin API |
| [`polyphon-ai.github.io/`](./polyphon-ai.github.io/) | Marketing and docs website | Hugo, deployed to polyphon.ai |

## How They Interact

### polyphon ↔ obsidian-polyphon (API contract)

`polyphon` exposes a **JSON-RPC 2.0 TCP API** on port 7432 (default). The Obsidian plugin connects to this socket and calls methods to authenticate, list compositions, manage sessions, and stream voice responses.

The type definitions in `obsidian-polyphon/src/types.ts` **manually mirror** `polyphon/src/shared/api.ts` and `polyphon/src/shared/types.ts`. When the Polyphon API changes, both files must be updated.

Key API methods used by the plugin:

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

### polyphon-ai.github.io → polyphon/obsidian-polyphon (documentation)

The site hosts all user-facing documentation for both projects:
- `content/docs/polyphon/` — main app docs
- `content/docs/integrations/obsidian-polyphon/` — plugin docs
- `content/docs/for-developers/api.md` — full JSON-RPC API reference
- `content/docs/for-developers/mcp.md` — MCP server docs

When API contracts or features change in either project, update the relevant docs here.

## Cross-Project Workflows

### Adding a new API method to polyphon
1. Implement in `polyphon/src/main/api/`
2. Add types to `polyphon/src/shared/api.ts`
3. If the Obsidian plugin will use the method, mirror types in `obsidian-polyphon/src/types.ts`
4. Update `polyphon-ai.github.io/content/docs/for-developers/api.md`

### Releasing a new version
1. Bump version in `polyphon` with `make bump-version VERSION=x.y.z`
2. Run `release.yml` — signs, notarizes, and publishes the macOS DMG
3. Run `update-download-version.yml` — updates the site and creates the release blog post

### Updating plugin or app documentation
- Plugin docs: `polyphon-ai.github.io/content/docs/integrations/obsidian-polyphon/`
- App docs: `polyphon-ai.github.io/content/docs/polyphon/`
- API reference: `polyphon-ai.github.io/content/docs/for-developers/api.md`

## Default Ports

| Service | Port |
|---|---|
| Polyphon JSON-RPC TCP API | 7432 |
