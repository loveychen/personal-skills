# Personal Skills

个人提效技能库：把经常重复的工作方法保存为可复用的 Agent Skills，按需安装到 Codex 或其他支持技能的助手。

## 技能目录

| Skill | 用途 | 调用示例 |
|---|---|---|
| [paper-deep-reading](skills/paper-deep-reading/SKILL.md) | 论文深度交互共读：由浅入深、公式与图表拆解、文献旁证、证据核查、断点续读 | `用 $paper-deep-reading 陪我精读这篇论文，从直觉开始逐步深入。` |

论文技能包含独立编写的流程和五份按需参考材料，不需要模型 API key 或额外服务。方法依据见 [来源与取舍](skills/paper-deep-reading/references/sources.md)，验证范围见 [验证记录](docs/validation.md)。

## 快速开始

本库按个人自用创建为私有仓库。克隆和安装需要当前 GitHub 账号有访问权限；登录网页不一定代表终端已经具备 Git 认证。

### 方式一：本地副本安装（适合当前已手工安装的环境）

```bash
git clone https://github.com/loveychen/personal-skills.git ~/personal-skills
cd ~/personal-skills

skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_root"
if [ -e "$skill_root/paper-deep-reading" ] || [ -L "$skill_root/paper-deep-reading" ]; then
  printf '%s\n' '已有安装，请按管理指南执行更新，避免覆盖本地修改。'
else
  cp -R skills/paper-deep-reading "$skill_root/paper-deep-reading"
fi
```

当前电脑已存在的 `paper-deep-reading` 可以继续使用，无需为保存到 GitHub 再安装一次。完整操作见 [安装、更新、卸载和回滚](docs/management.md)。

### 方式二：Skills CLI 管理（适合新环境）

需要 Node.js/npm 和能读取本私有仓库的 Git 认证：

```bash
# 查看本库可安装技能
npx skills add https://github.com/loveychen/personal-skills --list

# 用户级安装，只面向 Codex
npx skills add https://github.com/loveychen/personal-skills --skill paper-deep-reading --global --agent codex

# 查看、更新、卸载
npx skills list --global
npx skills update paper-deep-reading --global
npx skills remove paper-deep-reading --global --agent codex
```

CLI 安装与手工安装是两套管理方式。CLI 当前为 Codex 使用 `~/.agents/skills`，前述本地副本安装使用 `${CODEX_HOME:-$HOME/.codex}/skills`；本会话环境已识别后者。不要在两个目录保留同名安装；切换前按[迁移说明](docs/management.md#切换安装方式)备份旧副本。CLI 更新只管理它记录的安装，不会自动更新手工复制的目录。

## 使用与维护

- 安装后可输入 `$paper-deep-reading`，或说“陪我由浅入深精读这篇论文”。
- 阅读中可说“继续”“补背景”“推公式”“查前作”“直接讲，不提问”。
- 阅读进度保存在论文项目内的 `.paper-reading/`，不会自动推送到本仓库。
- 修改仓库内容后提交并推送，再更新本机安装；`git pull` 只更新仓库工作副本。
- 新增技能见 [新增与维护技能](docs/adding-skills.md)。

## 仓库结构

```text
personal-skills/
├── README.md
├── CHANGELOG.md
├── docs/
│   ├── management.md
│   ├── adding-skills.md
│   └── validation.md
└── skills/
    └── paper-deep-reading/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
```

## 操作依据

文档核对日期：2026-10-16。技能目录发现与配置参考 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)；CLI 命令参考 [vercel-labs/skills 官方说明](https://github.com/vercel-labs/skills)。CLI 版本升级后若参数不同，以 `npx skills --help` 和子命令帮助为准。
