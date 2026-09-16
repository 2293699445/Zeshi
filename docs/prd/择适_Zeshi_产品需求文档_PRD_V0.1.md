# 《择适 Zeshi 产品需求文档 PRD V0.1》

> **产品：** 择适 Zeshi  
> **版本：** PRD V0.1  
> **阶段：** MVP / Before + Decision 核心闭环  
> **目标：** 先证明“AI 能不能帮助一个不懂某个品类的消费者，更可靠地完成一次购买决策”  
> **产品原则：** AI-Native、Agent-first、消费者利益优先、证据透明、结构化展示、不过早堆技术  
> **当前项目权重：** 70% Java 后端 + AI 工程学习，30% 产品验证

---

# 1. V0.1 产品目标

V0.1 不追求完整实现 Before → Buy → After → Ownership 全生命周期。

这一版只完成最核心的一件事：

> **用户表达一个真实购买需求后，择适能够主动补齐关键条件、识别风险、研究候选商品、给出有证据的推荐，并把结果以结构化购买决策报告展示出来。**

成功标准不是“能聊天”，而是：

1. 用户不需要提前懂这个品类；
2. Agent 能发现用户遗漏的重要条件；
3. Agent 能根据真实商品/公开信息进行研究；
4. 系统能区分“事实、推断、建议”；
5. 推荐结论能够解释“为什么适合你”；
6. 用户最终能做出明确购买决策。

---

# 2. V0.1 首批类目

首批只支持 3 个类目：

1. **即热式热水器**
2. **路由器**
3. **耳机**

选择原因：

- 热水器：适合训练环境约束、安全规则、硬条件判断；
- 路由器：适合训练场景分析、家庭画像、参数匹配；
- 耳机：适合验证中小额消费品、偏好型决策和用户体验。

这样可以避免产品一开始只会做“大家电”。

---

# 3. 目标用户

## 3.1 核心用户

- 第一次购买某类商品；
- 不熟悉参数；
- 害怕踩坑；
- 重视性价比；
- 希望少看评测、少做功课；
- 愿意告诉 AI 自己的真实需求和使用场景。

## 3.2 用户核心问题

用户不是单纯问：

> “哪款最好？”

真实问题通常是：

> “哪款最适合我？”

---

# 4. V0.1 核心用户旅程

```text
打开择适
  ↓
输入“我想买什么”
  ↓
AI 识别品类与购买目标
  ↓
生成需求卡片
  ↓
主动追问缺失的重要条件
  ↓
形成完整 Requirement Profile
  ↓
执行风险 / 兼容性检查
  ↓
搜索候选商品
  ↓
抓取并结构化商品信息
  ↓
分析证据 / 评价 / 风险
  ↓
生成候选 Top 3
  ↓
结构化对比
  ↓
给出最终推荐
  ↓
生成 Purchase Report
  ↓
用户：购买 / 收藏 / 继续比较 / 修改条件
```

---

# 5. 核心交互设计原则

## 5.1 不做“纯聊天框”

聊天只负责：

- 用户表达目标；
- AI 追问；
- 用户补充条件；
- 用户继续追问。

真正的决策结果必须通过前端组件展示。

整体体验建议采用：

```text
┌──────────────────────────────────────────────┐
│                  顶部导航                    │
├───────────────────┬──────────────────────────┤
│                   │                          │
│    AI 对话区       │       决策工作台         │
│                   │                          │
│  用户输入需求      │  需求卡片                │
│  AI追问            │  风险检查                │
│  用户补充          │  商品候选                │
│                   │  对比表                  │
│                   │  最终推荐                │
│                   │  证据                    │
│                   │                          │
└───────────────────┴──────────────────────────┘
```

移动端采用：

```text
对话
↓
结构化卡片
↓
对比 / 报告
```

而不是左右分栏。

---

# 6. 首页设计

首页不是传统电商搜索框。

## 6.1 首屏

标题：

> **今天想买什么？**

副标题：

> 不用先懂参数，告诉我你想解决什么问题。

输入示例：

- “刚搬家，预算 800，想买热水器。”
- “95 平三室一厅，路由器怎么选？”
- “预算 500，安卓手机，想买降噪耳机。”
- “这两个型号哪个更值得买？”

主要 CTA：

> **开始做购买决策**

## 6.2 快捷场景

首页展示：

- 第一次买家电
- 数码产品怎么选
- 帮我比较两个商品
- 看看这个商品值不值得买
- 预算有限怎么选
- 二手能不能买

---

# 7. Decision Session

每一次购买决策创建一个 `DecisionSession`。

例如：

> “购买即热热水器”

Session 中包含：

```text
用户目标
预算
场景
偏好
硬性约束
缺失信息
候选商品
证据
风险
最终推荐
决策状态
```

状态：

```text
CREATED
↓
COLLECTING_REQUIREMENT
↓
READY_FOR_RESEARCH
↓
RESEARCHING
↓
COMPARING
↓
DECISION_READY
↓
COMPLETED
```

异常状态：

```text
NEED_USER_INPUT
FAILED
CANCELLED
```

---

# 8. Requirement Card

AI 从对话中实时提取需求。

前端显示：

## 你的需求

| 维度 | 当前值 |
|---|---|
| 类目 | 即热式热水器 |
| 预算 | ¥500–800 |
| 使用人数 | 2 人 |
| 地区 | 广州 |
| 核心诉求 | 性价比 / 冬季够热 |
| 安装空间 | 较小 |
| 电路条件 | 待确认 |

用户可以直接点卡片修改。

---

# 9. Missing Information

Agent 不应该无脑追问所有问题。

Category Knowledge 判断：

> 哪些信息会真正改变推荐结果？

例如热水器：

```text
功率要求        高优先级
线路线径        高优先级
空开            高优先级
家庭人数        中优先级
颜色            低优先级
```

前端展示：

> **还差 2 个关键信息就可以开始研究**

- [ ] 热水器线路线径
- [ ] 空开规格

支持：

- 文本回答；
- 图片上传；
- “我不知道”。

如果用户选择“不知道”，Agent 应给出获取方式。

例如：

> “可以拍一下配电箱，我帮你先识别空开。”

---

# 10. Constraint & Risk Check

这是择适区别于普通 AI 导购的重要界面。

例如：

## 使用条件检查

✅ 预算：匹配  
✅ 使用人数：匹配  
⚠️ 冬季加热能力：需重点关注  
❌ 7000W 方案：当前电路条件不建议

每条结论都展开说明：

> **为什么？**

例如：

> 根据当前已知的 2.5mm² 支路与 C20 空开条件，不应直接推荐高功率机型。最终安装仍应由专业电工确认。

前端区分：

- 通过；
- 风险；
- 不兼容；
- 信息不足。

---

# 11. Candidate Products

Agent 完成研究后生成候选商品。

每张商品卡：

```text
商品图
品牌 + 型号

适配度：92%
当前参考价：¥699

核心优势：
• 适合当前预算
• 恒温能力较好
• 售后覆盖较广

主要风险：
• 安装辅材可能额外收费
• 北方低温场景能力一般

[查看详情]
[加入对比]
```

最多默认展示 3 个候选。

产品原则：

> 少而明确，而不是给用户 20 个选择。

---

# 12. Product Comparison

对比页面是 V0.1 的核心页面之一。

示例：

| 维度 | 商品 A | 商品 B | 商品 C |
|---|---|---|---|
| 适配度 | 92% | 84% | 78% |
| 参考价 | ¥699 | ¥749 | ¥629 |
| 功率 | 5500W | 5500W | 7000W |
| 适合当前电路 | ✅ | ✅ | ❌ |
| 恒温 | 优 | 优 | 良 |
| 安装风险 | 中 | 低 | 中 |
| 售后 | 优 | 优 | 中 |
| 性价比 | 高 | 中高 | 表面高 |
| 推荐级别 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |

AI 在表格上方给一句：

> **结论：商品 A 最适合你。**

表格下方继续解释：

> B 更省心，但比 A 贵约 ¥50；  
> C 虽然参数更高，但你的当前电路条件不适合。

---

# 13. Evidence Panel

任何重要结论都应该尽量能解释证据。

例如：

> **“安装辅材收费争议较多”**

展开：

```text
来源 1：平台用户评价
37 条相关反馈

来源 2：品牌安装说明
部分辅材不包含在基础安装费用

可信度：中高
```

Evidence 数据至少包括：

```text
source_type
source_name
source_url
collected_at
claim
confidence
```

产品原则：

> AI 不应该假装自己什么都知道。

信息不足时明确显示：

> **证据不足。**

---

# 14. Final Recommendation

最终页面不应该是一大段 Markdown。

采用结构化报告：

# 最终建议

## 🥇 最推荐：商品 A

**适配度：92%**

### 为什么适合你

- 符合 ¥800 预算；
- 当前家庭条件可使用；
- 2 人连续使用能力基本满足；
- 你偏好性价比而不是品牌溢价。

### 你需要接受的缺点

- 安装辅材费用可能不透明；
- 极端低水压场景需要额外确认。

### 为什么没选 B

> 更省心，但多花的钱对你的当前需求价值不大。

### 为什么不推荐 C

> 功率更高，但当前电气条件不适合。

### 购买建议

> **可以买，但建议价格 ≤ ¥699 时入手。**

按钮：

- 收藏这个方案
- 再比较一款
- 修改预算
- 我已经买了
- 继续问 AI

---

# 15. Consumer Profile

V0.1 开始构建最基础用户画像，但不追求复杂推荐系统。

## 15.1 显式信息

用户主动提供：

- 预算倾向；
- 品牌偏好；
- 二手接受度；
- 是否愿意等促销。

## 15.2 推断信息

例如：

```text
price_sensitivity = high
durability_preference = high
decision_style = concise
```

所有推断必须：

- 记录依据；
- 可修改；
- 可删除。

用户界面：

> **择适对你的了解**

而不是：

> “用户标签”。

---

# 16. AI Response Style

用户可以选择：

- 简洁结论型；
- 平衡型；
- 深度研究型。

系统后期可以根据行为调整默认值。

例如：

> “你最近更常查看详细分析，是否默认切换为深度模式？”

---

# 17. Agent 设计 V0.1

V0.1 不做复杂 Multi-Agent。

底层使用一个统一 `DecisionAgent`，内部拆成明确能力模块：

```text
DecisionAgent
│
├── RequirementExtractor
├── CategoryKnowledgeTool
├── ConstraintChecker
├── SearchTool
├── ProductResearchTool
├── EvidenceTool
├── ComparisonEngine
└── RecommendationGenerator
```

为什么不一开始多 Agent：

> 当前业务闭环还没有证明多 Agent 带来的收益，不为了技术展示增加复杂度。

---

# 18. Agent 执行流程

```text
User Message
↓
Intent / Category
↓
Load User Profile
↓
Load Category Schema
↓
Requirement Extraction
↓
Missing Requirement?
├── Yes → Ask User
└── No
     ↓
Constraint Pre-check
     ↓
Product Search
     ↓
Product Normalization
     ↓
Evidence Collection
     ↓
Structured Product Intelligence
     ↓
Constraint Check
     ↓
Recommendation
     ↓
Purchase Report
```

---

# 19. AI Cost Control V0.1

从第一版就记录，不等用户量大再补。

## 19.1 Model Routing

```text
Intent / Extraction
→ Small Model

Review / Summary
→ Mid Model

Final Decision
→ Strong Model（必要时）
```

## 19.2 Java 优先

以下不用 LLM：

- 数值计算；
- 条件过滤；
- 排序；
- 基础规则；
- 适配度部分计算；
- Token Budget 判断。

## 19.3 Agent Guard

每个 Session：

```text
max_model_calls
max_tool_calls
max_agent_steps
timeout
max_cost
```

超出预算：

> 降级 / 中止 / 请求用户补充。

---

# 20. Product Intelligence Cache

对于同一商品：

```text
第一次
Search
↓
Research
↓
LLM
↓
Structured Product Intelligence
↓
Storage
```

后续复用：

```text
Cache / DB
↓
检查新鲜度
↓
必要时增量更新
```

V0.1 必须设计该数据结构，但可以先采用 MySQL 实现。

---

# 21. V0.1 页面信息架构

```text
择适
│
├── 首页
│   ├── 购买需求输入
│   └── 快捷场景
│
├── Decision Workspace
│   ├── AI Chat
│   ├── Requirement Card
│   ├── Risk Check
│   ├── Candidates
│   ├── Compare
│   └── Final Report
│
├── 我的决策
│   ├── 进行中
│   └── 已完成
│
├── 我的画像
│   ├── 消费偏好
│   ├── Home Profile
│   └── 回复风格
│
└── 设置
```

Buy / After / Ownership 在 V0.1 只保留导航扩展位置，不正式开发。

---

# 22. 后端核心领域模型 V0.1

建议第一版包含：

```text
User
ConsumerProfile
HomeProfile
DecisionSession
Conversation
Message
Requirement
Category
CategorySchema
Product
ProductOffer
ProductEvidence
ProductIntelligence
Recommendation
AiTask
AiCall
ToolCall
```

后续再扩展：

```text
PriceWatch
Purchase
OwnedItem
Warranty
ReturnWindow
Maintenance
```

---

# 23. MVP 验收场景

## 场景 A：热水器

用户：

> “预算 800，两个人，广州，想买即热热水器。”

验收：

- 能识别关键缺失条件；
- 会主动询问电路；
- 能识别 C20 等信息；
- 不推荐明显不匹配的产品；
- 输出 2~3 个候选；
- 给出明确最终建议。

## 场景 B：路由器

用户：

> “95 平，三室一厅，宽带 1000M，买什么路由器？”

验收：

- 询问户型 / 路由器放置位置；
- 判断是否需要 Mesh；
- 不只是按照价格排序；
- 输出网络覆盖相关解释。

## 场景 C：耳机

用户：

> “安卓手机，预算 500，通勤降噪为主。”

验收：

- 询问系统 / 降噪 / 通话 / 佩戴需求；
- 不把高价自动等同高适配；
- 能处理偏好型商品。

---

# 24. 不在 V0.1 做的内容

明确不做：

- 完整多平台实时最低价；
- 自动购买；
- 完整 CPS；
- AfterBuy；
- 物流；
- 价保；
- 保修；
- Marketplace；
- Multi-Agent；
- 微服务；
- Kubernetes；
- 完整向量数据库平台；
- 大规模爬虫。

这些以后根据真实需求逐步加入。

---

# 25. V0.1 产品指标

首批私测重点关注：

### 完成率

用户是否完成一次完整决策。

### 关键问题发现率

AI 是否提出了用户之前没想到的重要问题。

### 推荐采纳率

推荐是否影响实际购买。

### 决策满意度

用户主观：

> “这次推荐是否真的有帮助？”

### 再使用意愿

> “下次买东西，你是否还会用择适？”

### 替代关系

最重要的问题：

> “如果没有择适，你原本会用什么？”

以及：

> “用了择适以后，还需要再去问豆包 / 千问 / GPT 吗？”

---

# 26. 技术学习映射

V0.1 不是一次性全部开发。

## 第一阶段

```text
Git
Maven
Spring Boot
MySQL
REST
用户 / Session / DecisionSession
```

## 第二阶段

```text
LLM API
Structured Output
Agent Runtime
Model Routing
AI Cost
```

## 第三阶段

```text
Search
Product
Evidence
Recommendation
RAG
```

## 第四阶段

```text
Redis
缓存
Agent Guard
```

项目继续按照既定 12 个 Sprint 逐步演进。

---

# 27. 下一份设计文档

PRD V0.1 确认后，进入：

> **《择适 Zeshi 页面信息架构与交互原型说明 V0.1》**

重点输出：

- 页面级线框；
- 首页；
- AI Decision Workspace；
- Requirement Card；
- Risk Check；
- 商品对比；
- Final Report；
- 移动端交互；
- Agent 执行中状态；
- 错误 / 超时 / 成本预算耗尽等异常体验。

再下一阶段才进入：

> **《择适 Zeshi 技术架构设计 V0.1》**

以及：

> 数据库 ER → API → Sprint 1 工程初始化。
