# 方法依据与技能取舍

整理日期：2026-10-16。以下是设计来源，非效果排行榜。外部技能按已读规则分析，未用同一真实论文做教学效果排名；安装量和热度不能证明有效。本技能独立归纳，未复制第三方技能全文。

## 阅读与学习研究

1. [Keshav, How to Read a Paper，2016 修订版](https://systems.cs.columbia.edu/ds2-class/papers/keshav-paper.pdf)。经验方法：借鉴由全局到细节、最后重建；不把三遍和时长设为配额。
2. [Carey 等, Ten simple rules for reading a scientific paper，2020](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008032)。经验指导：阅读目标、主动提问、图表与方法核查、查引用和讨论。
3. [Chi 等, Self-Explanations，1989](https://doi.org/10.1207/s15516709cog1302_1)。力学例题研究；本次核对出版页面摘要，未审阅全部实验细节。启发解释步骤理由与诊断缺口，不保证所有论文场景等效。
4. [Chi 与 Wylie, The ICAP Framework，2014](https://education.asu.edu/sites/default/files/lcl/chiwylie2014icap_2.pdf)。认知参与框架：借鉴生成解释与相互回应；聊天次数不是学习深度，不能据此宣称某 AI 导师已验证有效。
5. [Karpicke 与 Blunt, Retrieval Practice Produces More Learning than Elaborative Studying with Concept Mapping，2011](https://pubmed.ncbi.nlm.nih.gov/21252317/)。实验研究；本次核对摘要。支持适时闭卷重建的设计，不推成所有任务下绝对优越。
6. [Dunlosky 等, Improving Students’ Learning With Effective Learning Techniques，2013，APS 概览](https://www.psychologicalscience.org/publications/journals/pspi/learning-techniques.html/comment-page-1)。使用出版机构概览；启发检索与分散学习，具体限制需回原综述核查，不据此指定最优复习间隔。

## 已查阅的论文技能

| 来源 | 采用要点 | 本技能调整 |
|---|---|---|
| [techdou/paper-reading](https://github.com/techdou/paper-reading/blob/main/SKILL.md) | 研究逻辑、主张与证据 | 默认逐轮共读，报告/HTML 按需 |
| [ddhh-gif/paper-reading-skill](https://github.com/ddhh-gif/paper-reading-skill/blob/main/SKILL.md) | 数理直觉、变量类型、假设与推导意义 | 按当前需要引入，不每轮输出长笔记 |
| [MrGeDiao/paper-reading-zh](https://github.com/MrGeDiao/paper-reading-zh/blob/main/paper-reading-zh/SKILL.md) | 材料边界、类型适配、跨论文可比性 | 允许节选限域教学，不增加例行格式确认 |
| [K-Dense：scientific-critical-thinking](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/skills/scientific-critical-thinking/SKILL.md) | 混杂、统计、证据归属 | 按学科选检查点，不一律套医学分级 |
| [jam-cc/paper-review.skill](https://github.com/jam-cc/paper-review.skill/blob/main/SKILL.md) | 直接前作、公平性、可追溯批评 | 服务理解讨论，正式审稿走专门流程 |

这是针对“深度交互、由浅入深、旁征博引”的综合设计。以下为 1.1.0 的领域补充；无研究直接验证整个组合最优，行为检查不等于学习效果验证。来源均由本次主任务或研究子任务实际打开，读取范围如表所列；不是每次共读都要重读的固定书单。

## LLM / Agent 专项方法依据（2026-10-16 核对）

| 来源 | 实际读取范围 | 采用与限制 |
|---|---|---|
| [DeepSeekMath v2](https://arxiv.org/html/2402.03300v2) | §4.1.1–4.1.2 的目标、policy 角色、组内奖励；§3–4 相关评测文字 | 以一次更新连接符号与机制，分开 old/ref policy。是具体算法实例，不能替代后续变体原文 |
| [DPO v2](https://arxiv.org/html/2305.18290v2) | §4 目标推导、数据流程；Appendix A.2 | 理论假设、原式、梯度解释分开；不能将重参数化结论推广到无条件的所有偏好训练 |
| [ReAct v3](https://arxiv.org/html/2210.03629v3) | §2 行动/观察/上下文；§3 入口与相关附录结构 | 从一次交互而非模块名字理解 Agent；文中可见推理不自动等于内部因果过程 |
| [Agentless v2](https://arxiv.org/html/2407.01489v2) | §3 分阶段流程；§5.2 消融文字 | 简单流程是值得比较的具体基线，不证明复杂架构永远无益；数值只属于该版本与设置 |
| [HELM v1](https://arxiv.org/html/2211.09110v1) | §1/1.1、§6、§7 | 场景/指标覆盖、适配与公平性分别判断；同 prompt 不自动意味着所有意义的公平 |
| [AI Agents That Matter v1](https://arxiv.org/html/2407.01502v1) | §2、§4–6、Appendix A.1 的部分实现讨论 | 成绩与成本、简单重试基线、泛化层级和环境口径；对当时系统的分析，不是永恒排名 |
| [τ-bench v1](https://arxiv.org/html/2406.12045v1) | §1、§3–5 | pass@k/pass^k、数据库结果与策略遵守的差别；模拟用户不能代替真实部署证据 |
| [Scaling LLM Test-Time Compute Optimally v1](https://arxiv.org/html/2408.03314v1) | §1–4；§5.1 开头 | proposal/verifier、难度分层、oracle 与估计开销。实验不计难度估计开销，不能直接推部署最优 |
| [Lessons from the Trenches on Reproducible Evaluation of Language Models v1](https://arxiv.org/html/2405.14782v1) | §2.1–4.1 | 复原输入构造、解码、后处理、评分与 commit；一致测量不保证代理指标有效 |
| [Proving Test Set Contamination in Black Box Language Models v1](https://arxiv.org/html/2310.17623v1) | 引言、§2–3.1、§6 | 核查污染机制和检测假设；未检测到不等于无污染，检测还依赖可交换性与 log-prob 访问 |
| [Evaluating Large Language Models Trained on Code](https://arxiv.org/pdf/2107.03374) | §2.1 的 pass@k 估计，Appendix A 相关论证 | 区分候选覆盖和交付选择；不要用总体均值直接代替逐任务估计或独立性假设 |
| [Judging LLM-as-a-Judge v4](https://arxiv.org/html/2306.05685v4) | §3.3–3.4、§4 及相关方法段落 | 顺序、长度、自偏好与参考评分核查；当时模型的偏差值不能套给新 judge |
| [Language Models Don't Always Say What They Think v2](https://arxiv.org/html/2305.04388v2) | §2–3 的干预/忠实性方法、相关结果文字 | 流畅 CoT 不足以证实解释忠实；特定模型与干预结果，不能推所有可见解释都无用 |
| [Introducing SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/) | 设置、人工验证构建与环境问题讨论；未另读 rubric PDF | 核查隐藏测试、回归与环境。人工筛选不能保证完美 oracle；历史声明须结合后续审计 |
| [Why we no longer evaluate SWE-bench Verified](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/) | 缺陷抽样、污染调查、部分案例与讨论，未逐段审完所有轨迹 | 138 个被选中的反复失败任务不是全体 500 题的随机样本；不外推审计缺陷比例 |
| [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | task/trial/trajectory/outcome/harness 定义、指标、环境隔离与轨迹检查 | 厂商工程经验；启发协议描述，不能当独立验证的教育或跨系统效果结论 |
| [Quantifying infrastructure noise](https://www.anthropic.com/engineering/infrastructure-noise) | 资源配置实验、边界及其他方差来源 | 特定 coding eval 的第一方实验；硬件/资源可改变结果，幅度不能外推任意任务 |

## 共读、论证与技能编写补充

| 来源 | 实际读取范围 | 本技能采用与限制 |
|---|---|---|
| [Philip Levis, Reading a CS or EE Research Paper](https://stanford.edu/class/cs114/reading-levis.pdf) | 四页材料中的术语、多遍阅读、前作和评测 | 重建、理解、检查分开；固定时长和手写偏好不作硬规则 |
| [CMU Zhihao Jia, Advanced ML Systems introduction](https://www.cs.cmu.edu/~zhihaoj2/15-779/slides/01-course-introduction.pdf) | PDF 29–31 页的阅读问题与讨论要求 | 解释问题/困难/创新/支持，跨论文迁移；课程实践不是学习效果实验 |
| [NeurIPS 2025 Reviewer Guidelines](https://nips.cc/Conferences/2025/ReviewerGuidelines) | review form、置信度与最佳实践 | 善意总结、证据与可改变判断的问题；不引入会议行政步骤或评分 |
| [NeurIPS Paper Checklist](https://nips.cc/public/guides/PaperChecklist) | 完整清单，重点 §1–8 | 主张、限制、不确定性和计算成本；清单不是论文质量总分 |
| [Jennifer Widom, Tips for Writing Technical Papers](https://cs.stanford.edu/people/widom/paper-writing.html) | 叙事结构、实验、引文和附录建议 | 问题到机制到证据，用例贯穿；资深研究者经验，不强制五段式 |
| [Chi 等，Eliciting Self-Explanations，1994](https://education.asu.edu/sites/g/files/litvpz656/files/lcl/chideleeuwchiulavancher_3.pdf) | 原文摘要、方法、相关结果及提示附录；未审完所有编码分析 | 小样本中学生任务，实验实际学习时间不等；不作为 AI 论文导师普遍因果效果的证明 |
| [Karpicke & Blunt，2011 原文](https://learninglab.psych.purdue.edu/downloads/2011/2011_Karpicke_Blunt_Science.pdf) | 正文实验、时间安排和延迟测试；未读补充方法 | 支持适时回忆重建，任务是实验室科学文本，不是高级 ML 论文或 AI 导师整体方案 |
| [Agent Skills specification](https://agentskills.io/specification) | 完整提取的格式、资源与披露规范 | 触发元数据、精简正文、按需参考；是规范建议，不是教学效果证据 |
| [Anthropic Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) | 描述、条件分支、披露与评估/迭代；未逐个运行示例 | 只增加会改变决策的信息，避免死模板；部分细节只适用于 Claude |
| [OpenAI Build skills](https://learn.chatgpt.com/docs/build-skills) | 触发、渐进披露、创建/配置和最佳实践 | 主要触发词前置，维护范围；宿主行为可能更新 |
| [OpenAI Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills) | 成功条件、触发样例、轨迹检查与评分，未执行示例 harness | 分开路由、行为、效率与风格；本技能场景为适配设计，不等于经过验证的教学测量 |

不同来源支持不同层次：规范约束格式，课程/工程经验启发流程，原始实验支持局部命题。可比性、可复现性、测量有效性和泛化性四分法，以及批判性段落结构，是跨来源综合，不冒充某一来源的原句或普遍定律。
