# 安装、更新、卸载与回滚

仓库源文件、助手使用的安装副本、论文阅读笔记是三类不同内容。以下命令以 macOS/Linux 的 shell 为例。仓库私有时使用已经配置好的 GitHub HTTPS 或 SSH 认证，不把访问令牌写进仓库、命令示例或 URL。

## 本地副本方式

这套方式适合现有 `${CODEX_HOME:-$HOME/.codex}/skills` 安装，不依赖 Skills CLI 的安装记录。请在每段命令中重新设置变量，避免依赖上一次终端状态。

### 首次克隆与安装

如果还没有仓库工作副本：

```bash
git clone https://github.com/loveychen/personal-skills.git ~/personal-skills
```

如果使用 SSH，可改用：

```bash
git clone git@github.com:loveychen/personal-skills.git ~/personal-skills
```

在仓库根目录执行安装：

```bash
cd ~/personal-skills
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_root"
if [ -e "$skill_root/paper-deep-reading" ] || [ -L "$skill_root/paper-deep-reading" ]; then
  printf '%s\n' '已有安装；请先备份，再按更新步骤操作。'
else
  cp -R skills/paper-deep-reading "$skill_root/paper-deep-reading"
fi
```

复制完整技能目录，不只复制 `SKILL.md`。首次安装不覆盖已有目录。当前会话已发现 `.codex/skills` 的安装；新环境也可根据官方目录说明选择 `~/.agents/skills`，整套命令保持同一路径即可。

### 更新仓库副本

```bash
cd ~/personal-skills
git status --short
git pull --ff-only
```

有本地修改时先提交或另行备份，不能用强制重置丢弃。此时安装副本还没变化；继续下面一步才会更新助手使用的技能。

### 更新安装副本（保留旧版）

在仓库根目录执行。先确认上一条 `git pull --ff-only` 成功：

```bash
cd ~/personal-skills
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
backup_root="$HOME/.local/share/personal-skills/backups"
mkdir -p "$skill_root" "$backup_root"
if [ ! -f skills/paper-deep-reading/SKILL.md ]; then
  printf '%s\n' '未找到仓库中的技能，请检查当前目录。'
else
  backup_dir="$(mktemp -d "$backup_root/paper-deep-reading.XXXXXX")"
  if [ -e "$skill_root/paper-deep-reading" ] || [ -L "$skill_root/paper-deep-reading" ]; then
    mv "$skill_root/paper-deep-reading" "$backup_dir/skill" &&
      cp -R skills/paper-deep-reading "$skill_root/paper-deep-reading"
  else
    cp -R skills/paper-deep-reading "$skill_root/paper-deep-reading"
  fi
  printf '旧版备份目录：%s\n' "$backup_dir"
fi
```

检查命令是否报错，再核对安装版本：

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
sed -n '1,12p' "$skill_root/paper-deep-reading/SKILL.md"
```

不要直接把新目录复制到已有同名目录内部，否则容易形成嵌套目录或留下被上游删除的旧文件。更新可能替换你的本地修改，所以修改优先维护在仓库源文件中。

### 卸载（保留备份）

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
backup_root="$HOME/.local/share/personal-skills/backups"
mkdir -p "$backup_root"
if [ -e "$skill_root/paper-deep-reading" ] || [ -L "$skill_root/paper-deep-reading" ]; then
  backup_dir="$(mktemp -d "$backup_root/paper-deep-reading.XXXXXX")"
  mv "$skill_root/paper-deep-reading" "$backup_dir/skill"
  printf '已从技能目录移出，备份在：%s\n' "$backup_dir/skill"
else
  printf '%s\n' '该目录未安装此技能。'
fi
```

此操作只移出该技能，不删除其他技能、仓库源码或论文项目里的 `.paper-reading/`。若其他作用域仍有同名技能，需要单独确认对应路径。已有对话可能保留已加载内容，可开启新对话检查发现结果。

### 回滚或恢复卸载

先将当前安装按上述卸载方法移到新的备份目录，记录路径。然后把以下 `先前输出的备份目录` 替换为真实目录，且确认它含有 `skill/SKILL.md`：

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
restore_from="先前输出的备份目录"
mkdir -p "$skill_root"
if [ ! -f "$restore_from/skill/SKILL.md" ]; then
  printf '%s\n' '备份目录无效，请替换 restore_from。'
elif [ -e "$skill_root/paper-deep-reading" ] || [ -L "$skill_root/paper-deep-reading" ]; then
  printf '%s\n' '当前安装仍存在，请先移出并备份。'
else
  cp -R "$restore_from/skill" "$skill_root/paper-deep-reading"
fi
```

## Skills CLI 方式

适合希望用一个工具管理多种助手技能的新环境。需要 Node.js/npm，私有仓库另需可用 Git 认证。以下命令按 2026-10-16 官方说明核对；不保证你本机现有 CLI 版本相同。

| 操作 | 命令 |
|---|---|
| 查看本库技能 | `npx skills add https://github.com/loveychen/personal-skills --list` |
| 用户级安装到 Codex | `npx skills add https://github.com/loveychen/personal-skills --skill paper-deep-reading --global --agent codex` |
| 只安装到当前项目 | 在目标项目执行 `npx skills add https://github.com/loveychen/personal-skills --skill paper-deep-reading --agent codex` |
| 查看用户级安装 | `npx skills list --global` |
| 更新这一项 | `npx skills update paper-deep-reading --global` |
| 更新所有用户级技能 | `npx skills update --global` |
| 从 Codex 卸载这一项 | `npx skills remove paper-deep-reading --global --agent codex` |
| 为 Claude Code 安装 | `npx skills add https://github.com/loveychen/personal-skills --skill paper-deep-reading --global --agent claude-code` |

不带 `--global` 表示项目作用域；不要用全量卸载命令代替单项卸载。CLI 可使用链接或副本安装，以实际命令输出的目标路径为准。管理方式取决于安装记录，不能据本地文件名判断 CLI 能否更新。

私有库更新失败时，先用 `git ls-remote https://github.com/loveychen/personal-skills.git HEAD` 检查终端认证与网络，再核对 CLI 版本。必要时使用上面的本地副本流程；不可把认证失败或未检测到更新当作成功更新。

## 切换安装方式

当前环境已有 `.codex/skills/paper-deep-reading` 手工副本。保留此方式时，按本地副本流程更新即可。

如要切到 CLI：先备份并移出旧手工副本，再执行 CLI 安装，查看输出目标和 `npx skills list --global`。不要手动伪造 CLI 的锁文件。若安装失败，可从备份恢复旧副本。

从 CLI 切回手工方式：先用 CLI 卸载相应作用域的技能，再安装本地副本。两套方式不要交替覆盖同一个目录。

## 临时停用与故障排查

官方文档支持在 `~/.codex/config.toml` 中为技能添加以下条目；将路径换成安装输出的实际绝对路径，修改后重启 Codex：

```toml
[[skills.config]]
path = "/实际安装路径/paper-deep-reading/SKILL.md"
enabled = false
```

重新启用时改为 `true` 或移除对应条目，保留其他配置。技能未出现时检查 `SKILL.md`、YAML 的 `name`/`description`、完整参考文件、同名重复安装和禁用配置；官方说明 Codex 自动检测技能变化，未出现时可重启。

参考：[OpenAI 官方技能说明](https://learn.chatgpt.com/docs/build-skills)、[Skills CLI 官方文档](https://github.com/vercel-labs/skills)。
