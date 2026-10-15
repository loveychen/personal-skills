# 新增与维护技能

每个技能放在 `skills/<skill-name>/`，一个文件夹对应一个独立技能。技能名使用小写英文、数字和连字符；目录名与 `SKILL.md` 中的 `name` 保持一致。

## 最小结构

```text
skills/your-skill-name/
├── SKILL.md
├── agents/openai.yaml   # 可选：显示名称与调用提示
├── references/          # 可选：按需读取的流程与参考
├── scripts/             # 可选：真正需要的可执行工具
└── assets/              # 可选：输出使用的模板或素材
```

最小 `SKILL.md` 示例，使用前替换名称及触发条件：

```markdown
---
name: your-skill-name
description: Use when the user needs a clearly defined recurring task.
metadata:
  version: "1.0.0"
---

# 技能标题

说明目标、必要上下文、关键决策、输出和能力边界。
```

先明确“什么请求应该触发、什么请求不该触发”，再写能改变助手行为的规则。主文件保持精简，复杂分支放参考材料；无必要不增加脚本、密钥或服务依赖。模板示例不能未经替换就作为正式技能提交。

## 提交流程

1. 在仓库源文件中编辑，避免只改助手的安装副本。
2. 用真实或合成任务检查：是否触发正确、输出可用、缺资料时是否诚实、是否遵从用户改变节奏。
3. 更新 `metadata.version`、README 技能目录和 CHANGELOG。外部技能改编需保留许可证与来源；仅概念参考也记录出处。
4. 检查将提交的文件，不包含论文全文、阅读记录、账号信息、密钥和安装备份。
5. 提交并推送，然后按管理指南更新安装副本。

```bash
git status --short
git diff
git add skills/your-skill-name README.md CHANGELOG.md
git diff --cached
git commit -m "Add your-skill-name"
git push origin main
```

有未推送提交或分支冲突时先处理，禁止用强制推送代替正常同步。发布前应重新检查技能的行为；结构校验不能证明实际效果。

## 版本和回滚

每个技能独立记录版本。需要可重复安装某个历史状态时，可为仓库创建明确的 Git tag，并在安装时选择该 tag 对应的目录；先确认安装工具支持相应来源格式。

修改出问题时，仓库用 `git revert` 创建可审查的撤销提交并推送，本地安装按管理指南恢复备份或重新安装修复版本。不要直接改写已经共享的历史。
