# Product Expert

面向真实业务决策的端到端产品专家技能包。它从第一性原理出发，把业务、用户、需求、体验、数据、系统、商业化、组织协同和持续学习连接成一条可追溯的决策链，而不是只生成一份看似完整的 PRD。

## 核心能力

- 第一性原理与业务建模
- 市场、商业模式、定价、包装、GTM 与增长
- 用户研究、JTBD、机会识别与需求拆解
- 产品规划、优先级、路线图、原型和验证
- 指标契约、实验设计、留存与 SaaS 分析
- 领域模型、数据库、API、事件与埋点设计
- 产品运营、决策权、干系人协同与发布治理
- AI 产品、RAG、上下文工程与 Agent 工作流
- 预测校准、决策复盘与产品知识连续性

## 设计原则

1. 从需要做出的决策开始，而不是从用户提出的功能开始。
2. 区分事实、观察、推断和假设。
3. 保持从业务目标到发布决策的完整追溯关系。
4. 根据风险和可逆性决定研究与验证深度。
5. 一个任务选择一个主模式，只加载真正影响决策的支持模块。
6. 不把行业基准、框架默认值或统计阈值当作普遍真理。

## 工作模式

技能会根据任务自动选择诊断、战略、商业化、发现、定义、规划、验证、分析、产品运营、产品判断、系统设计、AI 系统、审计或完整产品蓝图模式。

简单问题不会被强制扩展为完整产品方案；跨领域问题则会共享同一套证据、指标、实体和决策记录，避免模块之间互相矛盾。

## 目录结构

```text
product-expert/
├── SKILL.md                  # 主入口、模式路由和质量门槛
├── agents/openai.yaml        # Codex 界面元数据
└── references/               # 按任务需要加载的专业模块
    ├── first-principles-and-business.md
    ├── commercialization-and-growth.md
    ├── discovery-and-requirements.md
    ├── planning-and-validation.md
    ├── product-analytics-and-experiments.md
    ├── data-and-architecture.md
    ├── organization-and-product-ops.md
    ├── delivery-and-governance.md
    ├── product-judgment-and-continuity.md
    ├── ai-product-extension.md
    ├── ai-context-and-agents.md
    └── artifact-templates.md
```

## 安装

将仓库克隆或复制到 Codex 技能目录：

```powershell
git clone https://github.com/qlhouseClub/product-expert.git "$env:USERPROFILE\.codex\skills\product-expert"
```

重启或刷新 Codex 后，即可通过自然语言触发技能。

## 使用示例

- “帮我判断这个需求背后真正的业务问题，并决定是否应该做。”
- “为这个 B2B SaaS 设计定价、套餐和进入市场策略。”
- “把这份访谈材料转成机会地图和可验证的产品需求。”
- “诊断留存下降，但先不要写完整 PRD。”
- “为这个功能设计领域模型、数据库、API 和埋点。”
- “设计一个带 RAG 和人工审核机制的 AI 客服产品。”
- “审查这份产品方案，找出证据、指标和交付链路中的断点。”

## Token 与上下文策略

`SKILL.md` 只保留共同原则、路由和质量门槛。商业化、分析、数据、组织和 AI 等专业知识放在独立引用模块中，按需加载。知识库总量不会在每次任务中全部进入上下文。

## 研究来源

部分能力经过 [PM Brain](https://github.com/andreaskelm/pm-brain)、[18F Guides](https://github.com/18F/guides)、[GrowthBook](https://github.com/growthbook/growthbook)、[OpenFeature](https://github.com/open-feature/spec) 和 [Open Data Contract Standard](https://github.com/bitol-io/open-data-contract-standard) 的交叉研究。技能只吸收通用思想，并保留对许可、版本和适用边界的判断。

## 状态

- YAML 元数据校验通过
- 本地引用链接校验通过
- 已进行跨商业化、AI、数据和组织协同的前向测试
