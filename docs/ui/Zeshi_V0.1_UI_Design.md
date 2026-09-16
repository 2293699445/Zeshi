# 《择适 Zeshi UI Design V0.1》

> **设计对象：** V0.1 Before + Decision MVP  
> **设计目标：** 让用户感受到“AI 在帮我做决策”，而不是“我在和机器人聊天”  
> **设计原则：** Outcome First / Evidence Visible / Calm Intelligence / Consumer-first

---

## 1. 视觉定位

择适不采用典型电商平台的高刺激红黄促销视觉，也不采用纯 AI 产品常见的“黑底 + 发光渐变”。

希望形成的感受是：

- **可信**：像一个认真帮你做功课的人；
- **克制**：不制造焦虑，不用“限时抢购”压迫用户；
- **专业但不冷**：参数可读、解释通俗；
- **消费者立场**：风险和“不建议买”与推荐同等显眼。

关键词：

> Calm / Rational / Helpful / Evidence-driven / Human

---

## 2. 品牌视觉

### 主色

- Brand Green: `#1F6F5F`
- Brand Soft: `#E7F2EF`

含义：理性、可靠、长期使用感，避免传统电商促销色。

### 中性色

- Text Primary: `#181B20`
- Text Secondary: `#69707D`
- Border: `#E4E7EC`
- Surface: `#FFFFFF`
- Background: `#F6F7FB`

### 状态色

- Success: `#1F7A54`
- Warning: `#A96613`
- Risk: `#A53C3C`

状态色只用于兼容性、风险和系统状态，不用于制造促销冲动。

---

## 3. 字体与层级

建议：

- 中文：系统字体 / PingFang SC / Microsoft YaHei
- 英文与数字：Inter

字号：

- Hero H1: 40–44px
- Page title: 24–28px
- Section title: 18–20px
- Body: 14–16px
- Metadata: 11–12px

规则：

> 结论 > 解释 > 证据 > 元信息

最终推荐必须一眼看到，证据允许继续下钻。

---

## 4. Layout

### Desktop

导航 + 双栏工作台：

```text
Sidebar 260
│
├── Home
├── Decision Workspace
├── Decisions
├── Profile
└── Settings

Main
└── Decision
    ├── AI Conversation 380
    └── Decision Board flexible
```

聊天区域不是主体，**Decision Board 才是主体**。

### Mobile

禁止强行左右分栏。

采用：

```text
Conversation
↓
Requirement Card
↓
Risk
↓
Candidates
↓
Compare
↓
Final Report
```

重要结构化卡片可固定为底部 Sheet / 全屏子页面。

---

## 5. 核心组件

### 5.1 Requirement Card

目的：把 AI 从自然语言理解到的内容“显性化”。

要求：

- 每个字段可编辑；
- 明确“已确认 / 推断 / 待补充”；
- 不把模型推断伪装成用户事实。

### 5.2 Compatibility Check

四个状态：

- Pass
- Warning
- Fail
- Unknown

必须允许用户展开“为什么”。

### 5.3 Product Candidate Card

默认最多 3 个。

必须同时展示：

- 适配度；
- 当前参考价；
- 3 个核心优势以内；
- 2 个核心风险以内。

不展示无意义参数墙。

### 5.4 Compare Table

只比较影响本用户决策的维度。

不是商品详情页参数全搬。

### 5.5 Evidence Drawer

重要结论支持展开来源：

- 平台/品牌；
- 用户评价；
- 专业评测；
- 采集日期；
- 置信度。

### 5.6 Final Recommendation

必须包含：

1. 最推荐什么；
2. 适配度；
3. 为什么适合；
4. 缺点；
5. 为什么没选其他；
6. 当前是否值得买；
7. 下一步动作。

---

## 6. Agent 状态设计

AI 不能长时间只显示“正在思考”。

应显示阶段：

```text
正在理解需求
正在检查使用条件
正在研究候选商品
正在核对用户反馈
正在比较
正在生成购买建议
```

如果失败：

```text
商品数据不足
→ 可以继续使用现有证据
→ 或让用户补充商品链接
```

如果达到 Agent Cost / Step 限制：

> “这次研究已经达到当前分析上限。我已经保留可靠结论，剩余两项信息证据不足。你可以补充商品链接后继续。”

不展示内部 Token 或技术错误给普通用户。

---

## 7. AI 与 UI 的职责边界

AI 负责：

- 解释；
- 追问；
- 推理；
- 生成推荐理由。

UI 负责：

- 显示事实；
- 显示状态；
- 显示比较；
- 显示证据；
- 提供修改入口；
- 提供明确动作。

原则：

> 能用 UI 表达的稳定结构，不重复塞成长 Markdown。

---

## 8. 首页设计

Hero：

> 今天想买什么？

副文案：

> 不用先懂参数，告诉我你想解决什么问题。

输入框占视觉中心。

下方不展示商品 Feed，展示“真实场景”：

- 第一次买家电；
- 比较两个商品；
- 预算有限怎么选；
- 看看这个商品值不值得买；
- 二手是否值得买。

目的：强化“决策工具”而非“商城”。

---

## 9. Decision Workspace

核心视觉层级：

1. Requirement
2. Compatibility
3. Candidates
4. Comparison
5. Recommendation

每完成一个阶段，下一层渐进出现。

用户能够直观看到：

> AI 现在做到了哪一步。

这比一串聊天消息更容易建立信任。

---

## 10. Motion

只使用功能性动效：

- 新卡片 150–250ms fade/slide；
- Agent 阶段变化；
- Requirement 补齐进度；
- 报告生成后轻量展开。

禁止过多 Loading 动画、AI 粒子、发光球等装饰。

---

## 11. Accessibility

- 正文对比度满足可读性；
- 风险状态不能只依赖颜色，还使用图标和文字；
- 点击目标 ≥ 40px；
- 移动端核心按钮不小于 44px 高；
- 对比表在移动端改为卡片切换，不强塞横表。

---

## 12. V0.1 UI Screen List

正式开发前至少完成：

1. Home
2. Decision Workspace / Collecting Requirement
3. Decision Workspace / Risk Identified
4. Decision Workspace / Research
5. Product Comparison
6. Final Recommendation
7. Decisions History
8. Consumer Profile
9. Empty / Error / Evidence Insufficient
10. Mobile adaptations

当前交互 HTML 已覆盖 1–6 的主流程，7–10 在后续 UI 原型修订中补齐。

---

## 13. 前端实现建议

首版允许：

- React/Vue 任一；
- CSS Variables 管理 Design Token；
- 组件优先；
- 不引入沉重 Design System；
- 保留未来移动端复用可能。

推荐组件树：

```text
DecisionWorkspace
├── ConversationPanel
├── RequirementCard
├── ConstraintCheck
├── CandidateList
│   └── ProductCard
├── ProductCompare
├── EvidenceDrawer
└── RecommendationReport
```

---

## 14. 设计验收标准

一个第一次打开产品的人，应在 10 秒内理解：

> 这不是商城，而是帮我做购买决策的 AI。

完成一次决策后，应能够回答：

- AI 理解了我的哪些需求？
- 哪些条件阻止我买某个商品？
- 为什么推荐 A 而不是 B？
- 结论依据是什么？
- 我下一步该做什么？

如果这些答案只能从聊天记录里找，UI 设计失败。
