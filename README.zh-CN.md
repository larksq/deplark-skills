# Deplark / 速栈部署 Skill

**在 Codex 或 Claude Code 中，把本地网站或 Node.js 应用发布为可访问的站点。** 安装一次，连接自己的速栈账号，即可在多个项目中复用。

[开始使用](https://deplark.com/?lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) · [English](README.md) · [查看 Skill 文件](skills/deplark/SKILL.md)

## 安装

需要 Node.js 24 或更新版本、Deplark 账号，以及 Codex 或 Claude Code。浏览器连接账号和持久凭据保存目前需要 macOS；其他系统使用已有账号 Key 通过 `DEPLARK_API_KEY` 注入。不要把 Key 放进聊天、源码或命令参数。

```sh
# Codex，安装到个人范围，可跨项目复用
npx skills add larksq/deplark-skills --skill deplark --agent codex --global

# Claude Code
npx skills add larksq/deplark-skills --skill deplark --agent claude-code --global
```

也可使用[速栈安装向导](https://deplark.com/app?view=account-skill&lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution)，查看完整文件、连接账号并检查实际安装。下载或安装文件不等于账号授权，也不会自动发布项目。

## 对 AI 说

> 使用 Deplark Skill 发布当前项目。先检查账号连接，让我选择新建项目或已有项目，再完成构建、部署，并打开实际网址确认结果。

Skill 支持账号连接、列出自己的项目、新建或绑定项目，以及部署静态构建产物或符合运行要求的 Node.js 应用。静态产物根目录须有 `index.html`；Node.js 产物须包含配置的入口和运行依赖，并使用注入的 `PORT` 监听 `0.0.0.0`。

已有连接可直接复用。首次连接返回浏览器授权地址，核对账号和跨项目权限后确认，再让 AI 继续。凭据与 Skill 文件分离；Mac 使用 Keychain 保存。每次发布使用单项目、单次部署、一小时有效的票据。

安装器使用 `--agent claude-code`；Skill 内客户端使用 `--agent claude`。Codex 的个人目录为 `~/.agents/skills/deplark/`，Claude Code 为 `~/.claude/skills/deplark/`。

## 公开包与服务

包内只有通用 `SKILL.md`、公开配置 `deplark.json` 和官方客户端 `scripts/deplark.mjs`，不包含发布者的账号、项目绑定或凭据。用户各自连接账号；项目选择保存在各代码目录的 `.deplark/project.json`，其中没有 Key。

本 Skill 免费安装，按 MIT 许可证分发。托管套餐、运行类型和用量费用以[速栈当前说明](https://deplark.com/?lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution)为准。它不授予账单、管理员、密钥管理或删除权限。卸载本地 Skill 不会删除站点；云端账号授权需单独撤销。

遇到安装问题可[提交 Issue](https://github.com/larksq/deplark-skills/issues)，仅附错误码、系统版本及脱敏信息。此仓库提供 Agent Skill 和本地客户端，尚无 MCP 服务端点。
