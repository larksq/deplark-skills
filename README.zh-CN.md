# Deplark / 速栈 · 快速部署站点，中国大陆高速访问

**在 Codex 或 Claude Code 中快速部署网站和 Node.js 应用，让中国大陆用户高速访问。** 安装一次，连接自己的速栈账号，即可在多个项目中复用。

[开始使用](https://deplark.com/?lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution) · [English](README.md) · [查看 Skill 文件](skills/deplark/SKILL.md)

[skills.sh 收录页](https://www.skills.sh/larksq/deplark-skills/deplark) · [agentskill.sh 收录页](https://agentskill.sh/@larksq/deplark) · [ClawHub 收录页](https://clawhub.ai/larksq/skills/deplark) · [下载 v1.0.3](https://github.com/larksq/deplark-skills/releases/tag/v1.0.3)

## 通过 skills.sh 安装

需要 Node.js 24 或更新版本、Deplark 账号，以及 Codex 或 Claude Code。浏览器连接账号和持久凭据保存目前需要 macOS；其他系统使用已有账号 Key 通过 `DEPLARK_API_KEY` 注入。不要把 Key 放进聊天、源码或命令参数。

```sh
# Codex，安装到个人范围，可跨项目复用
npx skills add larksq/deplark-skills --skill deplark --agent codex --global

# Claude Code
npx skills add larksq/deplark-skills --skill deplark --agent claude-code --global
```

也可使用[速栈安装向导](https://deplark.com/app?view=account-skill&lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution)，查看完整文件、连接账号并检查实际安装。下载或安装文件不等于账号授权，也不会自动发布项目。

网页向导核验的是该次设置会话生成的完整文件；完成网页核验时使用该会话提供的包。市场发行版的介绍文案可能与向导版本不同。

## 对 AI 说

> 使用 Deplark Skill 快速部署当前站点，让中国大陆用户高速访问。先检查账号连接，让我选择新建项目或已有项目，再完成构建、部署，并打开实际网址确认结果。

Skill 支持账号连接、列出自己的项目、新建或绑定项目，以及部署静态构建产物或符合运行要求的 Node.js 应用。静态产物根目录须有 `index.html`；Node.js 产物须包含配置的入口和运行依赖，并使用注入的 `PORT` 监听 `0.0.0.0`。

已有连接可直接复用。首次连接返回浏览器授权地址，核对账号和跨项目权限后确认，再让 AI 继续。凭据与 Skill 文件分离；Mac 使用 Keychain 保存。每次发布使用单项目、单次部署、一小时有效的票据。

所需本机能力包括运行 Node.js 和项目构建命令、读取选定项目、写入构建产物与本地绑定，以及通过 HTTPS 连接 `deplark.com`。客户端通过 Mac 的 `/usr/bin/security` 读写 Deplark 专用 Keychain 条目，服务名为 `com.deplark.account-skills` 或兼容的 `com.deplark.skills`；条目标识由服务域名、授权范围与 AI 工具计算。AI 工具本身的调用权限和速栈账号授权仍分别受其各自规则控制。

安装器使用 `--agent claude-code`；Skill 内客户端使用 `--agent claude`。Codex 的个人目录为 `~/.agents/skills/deplark/`，Claude Code 为 `~/.claude/skills/deplark/`。

## 公开包与服务

包内只有通用 `SKILL.md`、公开配置 `deplark.json` 和官方客户端 `scripts/deplark.mjs`，不包含发布者的账号、项目绑定或凭据。用户各自连接账号；项目选择保存在各代码目录的 `.deplark/project.json`，其中没有 Key。

本 Skill 免费安装，按 MIT 许可证分发。托管套餐、运行类型和用量费用以[速栈当前说明](https://deplark.com/?lang=zh&utm_source=github&utm_medium=skill&utm_campaign=skill_distribution)为准。它不授予账单、管理员、密钥管理或删除权限。卸载本地 Skill 不会删除站点；云端账号授权需单独撤销。

遇到安装问题可[提交 Issue](https://github.com/larksq/deplark-skills/issues)，仅附错误码、系统版本及脱敏信息。此仓库提供 Agent Skill 和本地客户端，尚无 MCP 服务端点。

## 渠道分发包

各版本内置来源标记，首次浏览器连接自动携带，不需要用户选择渠道或填写参数。

| 分发渠道 | 包内来源 | 安装入口 |
| --- | --- | --- |
| skills.sh | `skills-sh` | 上面的 `npx skills add` 命令 |
| agentskill.sh | `agentskill` | [市场页面](https://agentskill.sh/@larksq/deplark)，使用[专用发布源](https://github.com/larksq/deplark-agentskill) |
| ClawHub | `clawhub` | [ClawHub 分发包](https://clawhub.ai/larksq/skills/deplark) |
| GitHub ZIP | `github` | [Release ZIP](https://github.com/larksq/deplark-skills/releases/tag/v1.0.3) |

仓库中的 `skills/deplark` 是 skills.sh 版，Release ZIP 是 GitHub 版。这里识别用户实际选择的分发渠道，不推测最早在哪里听说产品。本 GitHub README 的网站直达入口仍标记 `github`。

浏览器首次已识别来源保留 30 天，创建新账号后固定保存。更早的带标记网站访问优先于后来的安装包连接，重复登录不计新增。旧版无标记包不能追溯历史来源。
