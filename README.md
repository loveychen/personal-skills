# 个人提效技能库

个人提效技能库：把经常重复的工作方法保存为可复用的 Agent Skills，按需安装到 Codex 或其他支持技能的助手。

## 技能目录

| 技能 | 用途 | 调用示例 |
|---|---|---|
| [paper-deep-reading](skills/paper-deep-reading/SKILL.md) | 聚焦大型语言模型与智能体：用二维或三维动态图交互精读概念，核对机制、实验与前作，形成批判性笔记并断点续读 | `用 $paper-deep-reading 陪我精读这篇论文，并为适合的核心概念生成可控制的二维或三维动态图。` |
| [debate-driven-design](skills/debate-driven-design/SKILL.md) · [使用手册](skills/debate-driven-design/docs/usage.html) | 组织多角色质询、查证和多轮修订，形成有依据且各方明确接受的具体方案 | `使用 $debate-driven-design，比较这两个方案并推进到明确结论，保留验证边界。` |
| [prompt-coach](skills/prompt-coach/SKILL.md) · [使用手册](skills/prompt-coach/docs/usage.html) | 交付后复盘指令、提供两个完整后续请求，也支持按需练习批判性思考 | `使用 $prompt-coach，复盘我这次指令，并给出两个可直接使用的下一步请求。` |

论文技能当前为 **1.2.0**，描述与界面文案统一为中文，包含九份按需参考材料。新增 [动态解释规范](skills/paper-deep-reading/references/visual-explanations.md)：实际生成可暂停、逐步观察或调参的交互式动态图；三维支持画布直接拖拽旋转、缩放及复原视角，二维按需支持拖动参数、时间轴、节点或平移缩放。图中标明教学简化与论文数据，二维讲得清时不强加三维。无需额外模型服务或密钥，非人工智能论文也保留通用路径。方法依据见 [来源与取舍](skills/paper-deep-reading/references/sources.md)，专项调研见 [阅读方法研究](docs/research/llm-agent-paper-reading.md)，历史检查见 [1.1.0 记录](docs/validation-v1.1.md)，本次检查见 [维护与动态解释验证](docs/validation-maintenance.md)。

两个新增技能按 2026-11-11 的来源工作区快照同步，保留包内 MIT 许可证、参考资料和独立 HTML 手册。同步范围、结构检查与未验证项见[同步验证记录](docs/validation-skills-sync-20261111.md)。

## 项目维护技能

项目协作规则在 [AGENTS.md](AGENTS.md)。以下技能位于 `.agents/skills/`，用于维护本仓库，未安装到全局：

| 技能 | 用途 | 调用 |
|---|---|---|
| [技能设计](.agents/skills/personal-skill-design/SKILL.md) | 界定需求、触发、最小结构与验证场景 | `$personal-skill-design` |
| [技能评审](.agents/skills/personal-skill-review/SKILL.md) | 定位范围、规则、证据与维护成本问题 | `$personal-skill-review` |
| [技能验证发布](.agents/skills/personal-skill-release/SKILL.md) | 按改动验证，并在授权范围内同步安装和仓库 | `$personal-skill-release` |

在本仓库或其子目录开展任务时使用；不要把仓库维护技能当作论文阅读技能安装到所有项目。完整约定见 [质量检查](docs/quality-gates.md)。

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
- 技能编写方法见 [Skills 写作技巧](docs/skill-authoring-practices.md)；阅读评论的具体写法见 [批判性思考与写作](skills/paper-deep-reading/references/critical-writing.md)。

## 仓库结构

```text
personal-skills/
├── AGENTS.md
├── .agents/skills/
│   ├── personal-skill-design/
│   ├── personal-skill-review/
│   └── personal-skill-release/
├── README.md
├── CHANGELOG.md
├── docs/
│   ├── management.md
│   ├── adding-skills.md
│   ├── skill-authoring-practices.md
│   ├── quality-gates.md
│   ├── research/llm-agent-paper-reading.md
│   ├── validation.md
│   ├── validation-v1.1.md
│   └── validation-maintenance.md
├── evals/
│   ├── paper-deep-reading/
│   ├── debate-driven-design/cases.json
│   └── prompt-coach/cases.json
└── skills/
    ├── debate-driven-design/ # 含参考、许可证和 HTML 手册
    ├── prompt-coach/         # 含参考、许可证和 HTML 手册
    └── paper-deep-reading/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
```

## 操作依据

文档核对日期：2026-10-16。技能目录发现与配置参考 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)；CLI 命令参考 [vercel-labs/skills 官方说明](https://github.com/vercel-labs/skills)。CLI 版本升级后若参数不同，以 `npx skills --help` 和子命令帮助为准。
