# 可核实的实践来源

核验日期：2026-10-26。以下是短摘要和定位，不是完整原文或作者背书。按本次任务选择一两项；不要把全部条目塞进每次附录。来源中针对具体模型的行为建议须重新核对，稳定的任务表达原则可以借鉴。

## 1. 从交付结果反向改进指令

- 来源：Noah MacCallum、Brian Fioca，OpenAI，[Codex Prompting Guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide#metaprompting-for-targeted-fixes)，章节 `Metaprompting for targeted fixes`。
- 原则摘要：一轮表现不理想后，可要求模型针对观察到的问题提出指令调整；建议可能过拟合单个案例，应使用评估确认效果。
- 适用：本次确实观察到范围偏移、慢启动、冗余输出等问题时，针对具体问题讨论。该指南原本面向 API 与特定 Codex 版本，不能全盘搬用其系统提示。
- 本 Skill 的设计推导：只给候选改写，保留执行错误与环境限制的归因，不把自评当作改写有效的证明。

## 2. 明确验收信号与具体情境

- 来源：Anthropic，[Best practices for Claude Code](https://code.claude.com/docs/en/best-practices)，章节 `Give Claude a way to verify its work`、`Provide specific context in your prompts`。
- 原则摘要：提供可检查的目标、相关情境与已有参考，能使代理的执行和校验更具体；小而清晰的任务无需强制规划阶段。
- 原文短例：`fix it and verify the build succeeds`（原网页构建失败示例的片段，非完整提示词）。
- 适用：修 bug、改界面、产出报告时，把“做好”变为用户能判断的行为或交付要求。迁移到其他助手时，不照搬 Claude 专有命令和 hooks。
- 本任务改写方式：描述可观察结果；代码事实、可用命令由代理自行定位。UI 目标需要视觉证据时才加入视觉检查。

## 3. 用短指令激活已有工程习惯

- 来源：Simon Willison，[First run the tests](https://simonwillison.net/guides/agentic-engineering-patterns/first-run-the-tests/)，正文开头与提示词示例。
- 作者公开使用的短指令：`First run the tests`。
- 原则摘要：在已有工程中，测试能提供基线，也帮助代理理解项目；短指令可以表达已有工程实践。
- 适用：需要确认基线且确有可运行测试的代码变更。此例不是所有任务的固定开场，不给无关文案任务加测试，也不重复已经有效的检查。
- 本任务改写方式：必要时明确“先确认相关基线，再验证变更影响”；不编造项目测试命令。

## 4. 区分代理可查事实与用户需要决定的事

- 来源：Matt Pocock，[grilling / SKILL.md](https://github.com/mattpocock/skills/blob/5beb35b040e3de97e54fa9e386d7e42d15c295c2/skills/productivity/grilling/SKILL.md)。已读取原仓库入口，源文件 blob SHA `df69d9936880cd3314c28858c6c52f48db23b856`。
- 原则摘要：事实由代理调查；决策需要用户参与，问题之间有依赖关系。
- 适用：方向或取舍会实质改变交付的任务。用户无需在第一条指令中预先调查所有代码事实。
- 本地取舍：原 Skill 倾向穷尽访谈并等待确认；本 Skill 只借鉴事实/决定的区分，不把该访谈流程设为日常任务前置条件。

## 5. 减少无用约束，说明完成边界

- 来源：Eric Provencher，OpenAI，[Rethinking skills and prompts for GPT-6 Astra](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra)，章节 `Better skills`、`Up-to-date AGENTS.md`、`Persistence`。
- 原则摘要：过宽的 Skill 描述、无关材料与过细操作步骤会占用上下文或限制判断；持续执行的边界要贴合实际工作。
- 适用：用户提示词已堆满通用口号，或任务已清晰却仍建议增加模板时。文章针对特定模型，不能推断所有模型都无需验证提示。
- 本任务改写方式：保留目标和必要边界，删除没有影响判断的重复内容。说明交付到分析、实现、验证或上线的哪一步，以当前授权为准。

## 6. 先判断提示词是否是合适的改进对象

- 来源：Anthropic，[Prompt engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)，章节 `Before prompt engineering`、`When to prompt engineer`。
- 原则摘要：改进需要明确成功标准、可验证方法和原始提示词；并非所有失败都适合通过提示词解决。
- 适用：出现服务不可用、权限不足、模型能力不足，或请求已清晰但代理没有遵守的情况。
- 本 Skill 的设计推导：把提示词缺项、执行错误和环境限制分开。没有对照实验时只说候选收益，不宣称“这句补上就能避免失败”。

## 7. 把反馈连接到目标、当前差距与下一步

- 来源：John Hattie、Helen Timperley（2007），[The Power of Feedback](https://assess.ucr.edu/sites/g/files/rcwecm2336/files/2019-02/hattietimperley_2007.pdf)，期刊 pp. 86–90，Figure 1 与反馈层次讨论；2026-10-26 已读原文。
- 原则摘要：反馈应连接目标、当前进展与后续行动，并区分针对任务/过程的信息和对学习者个人的评价。
- 本 Skill 的设计推导：从本轮具体指令和结果解释一项可迁移的选择，把下一步连接到用户要推进的目标；不以泛泛赞扬代替教学。
- 迁移边界：这是一篇教育反馈综述，不是 Codex 提示词实验。可借鉴组织反馈的思路，不能据此宣称本 Skill 已改善用户学习或业务结果。

## 8. 说明如何改、为什么，而不只判断好坏

- 来源：Valerie J. Shute（2008），[Focus on Formative Feedback](https://myweb.fsu.edu/vshute/pdf/shute%202008_b.pdf)，期刊 p. 177，Table 2；作者大学主页提供的原文，2026-10-26 已核验。
- 原则摘要：反馈聚焦任务的具体特征，解释问题与改进方式；内容应足够具体、可理解，同时控制信息负担。
- 本 Skill 的设计推导：理由说明某项措辞或后续行动如何影响判断，不仅写“更明确”“符合最佳实践”；按需要解释关键机制与边界，而不机械增加字数。
- 迁移边界：关于教学反馈的结论不直接证明某次指令改写有效；候选收益仍需实际使用或同条件比较，不能把解释更完整等同于效果已验证。
