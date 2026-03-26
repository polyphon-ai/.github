# polyphon-ai/.github

Organization-level configuration for the [polyphon-ai](https://github.com/polyphon-ai) GitHub organization.

## Contents

- `profile/README.md` — Organization profile displayed on the GitHub org page
- `CLAUDE.md` — Workspace-level context for [Claude Code](https://claude.ai/code)

## CLAUDE.md

`CLAUDE.md` describes the relationships between the projects in this organization so that Claude Code has full cross-project context when working in the workspace.

It is intended to be loaded from the **parent directory** that contains all sibling repos. Claude Code loads `CLAUDE.md` files hierarchically, so placing it (or a symlink to it) one level above the project directories makes it available across all of them.

### Setup

After cloning this repo alongside the other polyphon-ai repos, create a symlink in the parent directory:

```sh
# From the directory that contains polyphon/, obsidian-polyphon/, polyphon-ai.github.io/, and .github/
ln -s .github/CLAUDE.md CLAUDE.md
```

Expected layout:

```
polyphon-ai/
  .github/          ← this repo
    CLAUDE.md       ← real file
    profile/
  CLAUDE.md         ← symlink → .github/CLAUDE.md
  polyphon/
  obsidian-polyphon/
  polyphon-ai.github.io/
```
