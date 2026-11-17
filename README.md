<p align="center"><img src="assets/deplark-logo.svg" alt="Deplark" width="220"></p>

# Deploy from your AI coding agent

**Deplark / 速栈 turns a local website or Node.js app into a live site from Codex or Claude Code.** Install one deployment Skill, connect your own Deplark account, and reuse it across projects.

[Get started](https://deplark.com/?utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) · [中文说明](README.zh-CN.md) · [Read the Skill](skills/deplark/SKILL.md)

## Install

Requires Node.js 24 or newer and a Deplark account. Browser account connection and persistent credential storage currently require macOS. On other systems, use an existing account Key through `DEPLARK_API_KEY`; do not put it in chat, source code, or command arguments.

```sh
# Codex: personal installation, reusable across projects
npx skills add larksq/deplark-skills --skill deplark --agent codex --global

# Claude Code
npx skills add larksq/deplark-skills --skill deplark --agent claude-code --global
```

You can also [open the guided installer](https://deplark.com/app?view=account-skill&lang=en&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) to review the files, connect your account, and verify the installation. Installing the files does not grant account access or publish a project.

## Try it

Open the code directory in your AI tool and ask:

> Use the Deplark Skill to publish this project. First check my account connection and let me choose a new or existing Deplark project. Build the app, deploy the output, and verify the live URL.

The Skill guides the agent through account connection, project selection, building, deployment, and checking the returned site. Static builds need an `index.html` at the output root. Node.js builds need the configured server entry, bundled runtime dependencies, and a listener on `0.0.0.0` using the supplied `PORT`.

The client supports `codex` and `claude` as the `--agent` values. The installer's `claude-code` identifier and the client's `claude` identifier are different.

For example, after a personal Codex installation:

```sh
node ~/.agents/skills/deplark/scripts/deplark.mjs status --agent codex
node ~/.agents/skills/deplark/scripts/deplark.mjs connect --agent codex --no-open
# After confirming the account and permissions at the returned browser URL:
node ~/.agents/skills/deplark/scripts/deplark.mjs connect --agent codex --resume --no-open
node ~/.agents/skills/deplark/scripts/deplark.mjs check --agent codex
```

If `connect` reuses an existing connection, no browser approval or resume is needed. A new connection returns immediately with an authorization URL. Approve only the account and permissions you intend to use. For Claude Code, use `~/.claude/skills/deplark/` and `--agent claude`.

## What is included

| File | Purpose |
| --- | --- |
| `skills/deplark/SKILL.md` | Agent instructions for account connection, project selection, building, and publishing |
| `skills/deplark/deplark.json` | Public service endpoint and the official uploader's SHA-256 digest |
| `skills/deplark/scripts/deplark.mjs` | Dependency-free official Node.js client, matching the public Deplark client at release time |

The package has no account Key, project ID, personal account information, or site binding. Each user connects their own account. On macOS, account credentials are stored separately in Keychain. A deployment uses a one-project, one-deployment ticket valid for one hour. The uploader is downloaded from Deplark and its SHA-256 digest is checked before execution.

Local project selection is saved in `.deplark/project.json` without credentials. The Skill does not grant billing, administrator, secret-management, or deletion access. Removing the local Skill does not delete a deployed site or revoke cloud authorization; manage authorization separately in Deplark.

## Service and support

The Skill package is free to install under the MIT license. Deplark hosting plans, runtime availability, and usage charges are separate; consult [the current service terms and plans](https://deplark.com/?utm_source=github&utm_medium=skill&utm_campaign=skill_distribution). Public release updates are available in this repository. If the uploader changes, update the Skill package rather than disabling its integrity check.

For installation issues, [open an issue](https://github.com/larksq/deplark-skills/issues). Include the error code and your operating system; keep tokens, account data, source archives, and private URLs out of public reports.

This repository distributes an Agent Skill with a local client. It does not provide an MCP server endpoint.
