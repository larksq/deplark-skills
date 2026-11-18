<p align="center"><img src="assets/deplark-logo.svg" alt="Deplark" width="220"></p>

# Quickly deploy websites for fast access from mainland China

**Deplark / 速栈 quickly turns a local website or Node.js app into a live site with fast access from mainland China, using Codex or Claude Code.** Install one deployment Skill, connect your own Deplark account, and reuse it across projects.

[Get started](https://deplark.com/?utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) · [中文说明](README.zh-CN.md) · [Read the Skill](skills/deplark/SKILL.md)

[skills.sh](https://www.skills.sh/larksq/deplark-skills/deplark) · [agentskill.sh](https://agentskill.sh/@larksq/deplark) · [ClawHub](https://clawhub.ai/larksq/skills/deplark) · [Download v1.0.3](https://github.com/larksq/deplark-skills/releases/tag/v1.0.3)

## Install via skills.sh

Requires Node.js 24 or newer and a Deplark account. Browser account connection and persistent credential storage currently require macOS. On other systems, use an existing account Key through `DEPLARK_API_KEY`; do not put it in chat, source code, or command arguments.

```sh
# Codex: personal installation, reusable across projects
npx skills add larksq/deplark-skills --skill deplark --agent codex --global

# Claude Code
npx skills add larksq/deplark-skills --skill deplark --agent claude-code --global
```

You can also [open the guided installer](https://deplark.com/app?view=account-skill&lang=en&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) to review the files, connect your account, and verify the installation. Installing the files does not grant account access or publish a project.

The web wizard verifies the exact package generated for its setup session. Use that session's generated files for its verification flow; the marketplace release can have different introductory wording.

## Try it

Open the code directory in your AI tool and ask:

> Use the Deplark Skill to quickly publish this project for fast access from mainland China. First check my account connection and let me choose a new or existing Deplark project. Build the app, deploy the output, and verify the live URL.

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

The agent needs a local shell to run Node.js and the project's build commands, file access to inspect the selected project and write its build output and local binding, and HTTPS access to `deplark.com` for authorization and deployment. The client uses macOS `/usr/bin/security` to read and write Deplark-specific Keychain items under `com.deplark.account-skills` or the compatible `com.deplark.skills` service. Keychain item names are derived from the service origin, authorization scope, and selected AI tool. These requirements describe the client's behavior; your agent's own tool permissions and your Deplark account consent remain separate.

Local project selection is saved in `.deplark/project.json` without credentials. The Skill does not grant billing, administrator, secret-management, or deletion access. Removing the local Skill does not delete a deployed site or revoke cloud authorization; manage authorization separately in Deplark.

## Service and support

The Skill package is free to install under the MIT license. Deplark hosting plans, runtime availability, and usage charges are separate; consult [the current service terms and plans](https://deplark.com/?utm_source=github&utm_medium=skill&utm_campaign=skill_distribution). Public release updates are available in this repository. If the uploader changes, update the Skill package rather than disabling its integrity check.

For installation issues, [open an issue](https://github.com/larksq/deplark-skills/issues). Include the error code and your operating system; keep tokens, account data, source archives, and private URLs out of public reports.

This repository distributes an Agent Skill with a local client. It does not provide an MCP server endpoint.

## Distribution editions

Each edition carries its own registration source automatically; users do not need a source flag.

| Distribution | Package source | Installation |
| --- | --- | --- |
| skills.sh | `skills-sh` | The `npx skills add` commands above |
| agentskill.sh | `agentskill` | [Market listing](https://agentskill.sh/@larksq/deplark), from the [dedicated source](https://github.com/larksq/deplark-agentskill) |
| ClawHub | `clawhub` | [ClawHub package](https://clawhub.ai/larksq/skills/deplark) |
| GitHub ZIP | `github` | [Release ZIP](https://github.com/larksq/deplark-skills/releases/tag/v1.0.3) |

The repository's `skills/deplark` folder is the skills.sh edition; the release ZIP is the GitHub edition. This distinguishes the selected distribution from where a user may first have heard about Deplark. Direct website links in this GitHub README are tagged `github`.

Deplark retains the first identified website source for 30 days and records it once when a new account is created. An earlier tagged website visit takes precedence over a later package connection. Repeat sign-ins are not new users; old unlabelled packages cannot be retroactively attributed.
