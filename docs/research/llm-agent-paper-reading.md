# LLM / Agent 深度交互阅读：调研与设计依据

日期：2026-10-16。目标是优化个人 `paper-deep-reading`，服务持续跟进 AI 研究；不是列论文排行榜或宣称存在对所有人最优的阅读方法。

本轮围绕模型机制、评测归因、Agent 系统、交互学习、批判性写作和技能编写六个问题，打开并定点阅读了 17 项领域来源及 11 项方法/规范补充。原始来源、具体访问范围与限制见[技能来源表](../../skills/paper-deep-reading/references/sources.md)。未使用来源数量、star 或论文声望替代证据质量。

## 1. 理解对象要从“论文摘要”变成完整机制

LLM 论文的改进可能位于数据、模型、训练目标、解码、搜索、验证或评分。DeepSeekMath 的原始目标区分当前、采样旧策略和参考策略；DPO 的推导连接偏好假设与目标。阅读应先确定某个符号/模块在一次真实训练或推理中做什么，再讨论作者解释与实验支持，不能识别到算法名字就用记忆补原式。[DeepSeekMath §4.1](https://arxiv.org/html/2402.03300v2)、[DPO §4](https://arxiv.org/html/2305.18290v2)

Agent 阅读则先跟踪一次模型—工具—环境交互，区分上下文更新、实际状态改变和权重更新。ReAct 提供了这种轨迹视角；Agentless 表明在具体软件工程任务中，固定分阶段流程也是应考虑的对照。这些来源不证明任何架构普遍优越。[ReAct §2](https://arxiv.org/html/2210.03629v3)、[Agentless §3、§5.2](https://arxiv.org/html/2407.01489v2)

**落地：**新增 `llm-reading.md` 和 `agent-reading.md`，按论文贡献定位，再沿一次样本/更新/行动解释。入口只按需路由，不给每轮加入全套审查清单。

## 2. 分数提高需要先问“谁以什么预算完成了什么”

HELM 和 lm-eval 的研究分别强调覆盖、适配，以及输入构造、生成、后处理和评分细节。重复采样、强 verifier 与底座升级是不同因素。Test-time compute 研究还展示了 oracle 难度、预测难度与估计开销的区别；论文中的最优分配不自动是部署最优。[HELM §1、§6–7](https://arxiv.org/html/2211.09110v1)、[lm-eval §2–4](https://arxiv.org/html/2405.14782v1)、[Test-Time Compute §3.2](https://arxiv.org/html/2408.03314v1)

应分开判断：比较是否公平、别人能否复现、指标是否有效、结果能否泛化。模型快照、候选数、验证器、工具权限和总预算一起变，不能仅把差值归因于一个新目标。成本分析应与论文主张匹配，不把 token、价格、FLOPs 与时延当同一量。

**落地：**记录最关键协议与信息边界，核对相同预算/质量的口径；比较训练和部署时分开。对 oracle、选择与难度估计成本增加专门检查。

## 3. Agent 的“成功”“可靠”和“遵守规则”是不同命题

τ-bench 区分至少一次成功和所有重复尝试成功，并指出最终数据库状态评分可能遗漏必要确认等过程要求。工程评测文档进一步区分任务、尝试、轨迹、最终环境结果，以及 agent harness 与 evaluation harness。[τ-bench §3–5](https://arxiv.org/html/2406.12045v1)、[Anthropic agent evals](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

因此，五次取最佳不能直接证明单次或持续可靠；Agent 说完成不等于环境状态已正确。环境资源、残留文件/记忆、失败排除和人工介入也应核对。基础设施失败应单列，按评估目标决定如何计入，不一律算规划失败或全部删除。[AI Agents That Matter](https://arxiv.org/html/2407.01502v1)、[Infrastructure noise](https://www.anthropic.com/engineering/infrastructure-noise)

**落地：**先读成功与失败轨迹，验证真实状态与约束；把底座、控制、工具、环境和评分因素拆开，并保存重要配置。

## 4. 批判性写作需要把推论连接写出来

NeurIPS 的指导要求准确重述贡献、以依据评价，并提出有用的问题。Widom 和 Levis 的建议分别提供问题到贡献的叙事，以及理解与检查分离的阅读方式。这些是规范/经验，不能当教学效果实验。[NeurIPS reviewer guide](https://nips.cc/Conferences/2025/ReviewerGuidelines)、[Widom](https://cs.stanford.edu/people/widom/paper-writing.html)、[Levis](https://stanford.edu/class/cs114/reading-levis.pdf)

一条有价值的批评应说明：作者哪项主张，原文出现什么现象，为什么影响该结论，还有什么替代解释，以及什么证据能改变判断。缺少说明与证明失败不同；没有独立消融不自动否定组合系统的实际价值。有支持局部贡献的良好对照时，应明确肯定，不能凑缺点。

LLM judge 的一致意见不自动等于正确，流畅 CoT 也不自动等于忠实解释；应分别核对评分器偏差及干预证据。既有论文对特定模型的结果不能机械套给当前模型。[LLM-as-a-Judge §3.3–3.4](https://arxiv.org/html/2306.05685v4)、[CoT faithfulness §2–3](https://arxiv.org/html/2305.04388v2)

**落地：**新增 `critical-writing.md`，提供证据到推论的段落结构、校准措辞、正面评价和可改变判断的检查；正式审稿仍使用专门流程。

## 5. 文献扩展围绕机制和争议，而非堆经典名词

课程阅读要求和已有方法指南支持先概括问题、困难、贡献与支持，再做比较、迁移和综合。[CMU Advanced ML Systems 阅读问题](https://www.cs.cmu.edu/~zhihaoj2/15-779/slides/01-course-introduction.pdf)

对单篇论文，优先找到最近前作、直接替代方法、简单强基线、独立复核与必要后续修订。基准也会随暴露、实现和模型变化而失效，旧的人审结论不能永久充当有效性担保。尤其要看审计的抽样：SWE-bench 后续报告中选取的反复失败任务不是全基准随机样本，其缺陷比例不可无条件外推。[原始 Verified 说明](https://openai.com/index/introducing-swe-bench-verified/)、[后续审计](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/)

**落地：**记录技术关系、版本与核验日期；把建议研究写成假设和最小区分实验。检索未找到不是没有前作，未检出污染也不是证明无污染。[Contamination 检测研究的条件与限制](https://arxiv.org/html/2310.17623v1)

## 6. 交互教学和技能工程各自验证

自我解释和检索练习为让读者重建联系提供局部支持，但任务、学习者和研究设计限制很重要。Chi 1994 的研究存在实际学习时间不等；Karpicke & Blunt 2011 的科学文本实验也不是高级 ML 论文或 AI 导师实验。不能把整个“苏格拉底式共读”包装成已证明最优。[Chi 原文](https://education.asu.edu/sites/g/files/litvpz656/files/lcl/chideleeuwchiulavancher_3.pdf)、[Karpicke & Blunt 原文](https://learninglab.psych.purdue.edu/downloads/2011/2011_Karpicke_Blunt_Science.pdf)

技能工程采用紧凑入口、明确触发、直接参考和按需披露，评估显式、隐式、上下文及负向触发；行为测试与学习效果分开。正文的预算是建议，不靠堆规则保证可靠。[Agent Skills spec](https://agentskills.io/specification)、[Anthropic authoring guide](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)、[OpenAI skill evals](https://developers.openai.com/blog/eval-skills)

**落地：**一轮推动一个问题，参考材料按任务加载；尊重不提问、完整报告等偏好。维护者技能写作技巧放进仓库指南，避免让阅读技能变成同时负责“创建技能”的宽泛入口。

## 验证与边界

v1.0 的基线已能处理多项合成 LLM/Agent 证据问题，不能声称旧版必然失败。本轮新增的价值目标是把领域检查和写作决策显式化、降低初学者负担，并验证关键边界。实际测试、未覆盖项及示例重叠见[本轮验证记录](../validation-v1.1.md)。没有运行模型训练、基准复现或长期学习实验。
