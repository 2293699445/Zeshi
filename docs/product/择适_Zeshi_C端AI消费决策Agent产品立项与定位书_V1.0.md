# 《择适 Zeshi —— C端 AI 消费决策 Agent 产品立项与定位书 V1.0》

> **文档状态：** 立项草案 V1.0  
> **项目代号 / 产品工作名：** 择适（Zeshi）  
> **产品类型：** AI-Native Personal Consumer Agent / Personal Consumer OS  
> **当前主目标权重：** 70% Java 后端 + AI 工程学习，30% 产品验证与商业化探索  
> **当前阶段：** 学习项目 + 私测产品，不以短期盈利为成功标准  
> **长期目标：** 从“买什么”延伸到“什么时候买、在哪里买、买完怎么管、什么时候修/卖/换”，成为个人消费生命周期 Agent。

---

## 0. 为什么叫「择适」

“择适”表达的是这个产品最核心的立场：

> **不是帮用户买最贵、最热门、佣金最高的东西，而是帮用户选择真正适合自己的东西。**

产品口号暂定：

> **懂你所需，择你所适。**

另一条更消费者化的表达：

> **买得明白，用得长久。**

“择适”目前仅作为项目和产品工作名。正式商业发布前必须完成商标、域名、应用商店重名及近似名称检索，不把当前工作名视为已经取得品牌权利。

---

# 1. 项目立意

现代消费者面临的真正问题，不是“没有商品可以买”，而是：

- 商品太多；
- 参数太复杂；
- 平台各说各话；
- 广告、达人、商家利益立场混杂；
- 用户往往第一次接触某个品类；
- 用户不知道购买一个品类前“自己还不知道什么”；
- 购买前、购买中、购买后信息割裂。

例如一个第一次购买即热热水器的普通用户，可能只知道：

> “预算 800 元，两个人用，冬天想洗热一点。”

但真正影响购买决策的还有：

- 家庭线路线径；
- 空开容量；
- 电表条件；
- 最大功率；
- 冬季进水温度；
- 水压与流量；
- 安装空间；
- 安装辅材费用；
- 售后覆盖；
- 实际用户长期反馈。

普通消费者很难在购买前主动想到这些问题。

**择适的价值不是替用户搜索商品，而是替用户完成一次购买决策尽调。**

---

# 2. 产品一句话定义

**择适是一个站在消费者一边的 AI 消费 Agent：它理解用户、理解商品、理解价格和使用环境，并持续管理从购买决策到商品生命周期结束的全过程。**

---

# 3. 产品不是“AI 导购”

如果产品最终只是：

> 用户输入预算 → 模型推荐 3 个商品 → 跳转电商购买

那么它没有足够价值，也很容易被通用 AI 和电商平台自身能力取代。

择适必须形成完整的消费者工作流：

```text
Need
产生需求
   ↓
Before
购买需求澄清 / 类目知识 / 风险识别
   ↓
Decision
候选商品研究 / 证据 / 评价 / 适配度
   ↓
Buy
比价 / 优惠 / 历史价格 / 购买时机
   ↓
After
物流 / 价保 / 退换 / 保修 / 维修
   ↓
Ownership
物品资产 / 耗材 / 使用寿命 / 闲置
   ↓
Exit
二手出售 / 以旧换新 / 回收 / 淘汰
```

最终目标不是 BeforeBuy App，而是：

> **Personal Consumer OS**

---

# 4. 目标用户

早期核心用户不是“所有网购用户”，而是：

### 4.1 第一次独立生活的年轻人

例如：

- 第一次租房；
- 第一次搬家；
- 第一次装修；
- 第一次独居；
- 第一次成家；
- 第一次购买大型家电。

他们对品类知识明显不足，但消费决策很多。

### 4.2 价格敏感、重视性价比的人群

典型表达：

- “预算最好不要超过……”
- “性价比高一点。”
- “想耐用一些。”
- “有没有必要上这个配置？”
- “二手能买吗？”
- “618 会不会更便宜？”

系统不应该武断把用户标记为“消费能力不强”。

更合理的画像字段是：

```text
price_sensitivity = high
durability_preference = high
brand_premium_tolerance = low
used_goods_acceptance = medium
wait_for_discount = high
```

这些都是**可解释、可修改的消费偏好推断**。

### 4.3 数码 / 耳机 / 小家电 / 日用品消费者

产品不能只做大家电。

择适按“决策难度”决定分析深度，而不是按商品价格决定。

例如一副 ¥500 耳机仍然可能涉及：

- 手机系统；
- 编码；
- 降噪需求；
- 通话；
- 佩戴舒适度；
- 游戏延迟；
- 音乐偏好。

即使是低价商品，也可以提供轻量建议。

---

# 5. AI-Native 产品体验

## 5.1 用户不需要先学会这个品类

用户只需要说：

> “刚搬家，想买个热水器，预算 800。”

Agent 首先做的不是推荐，而是判断：

> “为了不买错，我还必须知道哪些信息？”

形成动态 Requirement Checklist。

---

## 5.2 系统主动发现“用户不知道自己不知道什么”

例如：

```text
用户：想买 7000W 即热热水器。
Agent：
→ 查询 Home Profile
→ 发现线路信息不完整
→ 询问线径 / 空开
→ 用户上传配电箱照片
→ Vision 提取 C20
→ Java Rule Engine 做安全约束计算
→ 判断当前条件不适合直接推荐 7000W
```

最终输出不是：

> “7000W 参数更强。”

而是：

> **“这款商品本身不错，但不适合你当前家庭条件。”**

---

# 6. Personal Profile：AI 要越来越懂用户

择适需要构建长期、结构化、可修改的消费画像。

## 6.1 Consumer Preference Profile

例如：

```text
价格敏感度：高
更重视：耐用 / 性价比
品牌溢价接受度：低
二手接受度：中
等待促销意愿：高
偏好：少推荐、明确结论
```

因此同一个问题：

> “AirPods Pro 值得买吗？”

不同用户得到的策略不同。

价格不敏感用户：

> “如果你重视苹果生态和使用省心，可以直接买。”

价格敏感用户：

> “目前价格处于常规区间，你并不急用。按你的购买偏好，更建议等 618 / 双11 或考虑成色较好的官方渠道二手。”

---

## 6.2 Home Profile

保存与家庭消费相关的稳定事实：

```text
城市
住房类型
家庭人数
住房面积
主要空间尺寸
网络环境
电气条件
家庭设备生态
```

以后购买：

- 热水器；
- 空调；
- 路由器；
- 洗衣机；
- 家具；

不必每次重新描述。

---

## 6.3 Response Style Profile

系统可以学习用户更喜欢什么表达方式，例如：

```text
detail_level = medium
decision_first = true
technical_explanation = medium
number_of_recommendations = 2
tone = direct
```

例如用户长期不喜欢长篇铺垫，系统以后优先：

> “结论：推荐 A，80%。理由有三个……”

而不是每次生成模板化长文。

### 边界

- 只学习表达偏好，不偷偷推断敏感人格；
- 用户可以查看和修改；
- 用户可以关闭个性化；
- 不用“迎合用户”替代事实判断。

---

# 7. Category Knowledge：类目购买知识

每种商品都拥有自己的购买决策 Schema。

### 即热热水器

```text
electricity
water_pressure
inlet_temperature
flow_rate
installation
power
safety
maintenance
after_sales
```

### 路由器

```text
house_area
house_layout
wall_material
broadband
device_count
wired_backhaul
mesh
wifi_standard
```

### 耳机

```text
phone_os
codec
anc
microphone
latency
comfort
music_preference
battery
multi_device
```

### 椅子

```text
height
weight
desk_height
sitting_time
lumbar_support
seat_depth
material
space
```

这会逐渐形成择适重要的数据资产：

> **Category Decision Knowledge Base**

---

# 8. Purchase Due Diligence

最终推荐不能只有“推荐 A”。

系统应生成结构化 Purchase Report：

```text
需求匹配度
硬性条件检查
推荐原因
不推荐原因
竞品比较
用户评价风险
价格
优惠
真实到手成本
长期使用成本
二手价值
售后
购买时机
证据来源
置信度
```

核心 UI：

> **推荐 A：92% 适合你**

并解释：

- 为什么适合；
- 为什么 B 没有被选；
- 哪些风险仍然未知；
- 结论依赖了哪些证据。

---

# 9. Price Agent

比价不能只做：

```text
京东 699
淘宝 679
```

应该计算：

```text
商品价
- 平台券
- 店铺券
- 补贴
- 返利
+ 运费
+ 安装
+ 必须配件
= 实际购买成本
```

后期加入：

### Total Cost of Ownership

例如：

```text
购买价格
+ 5 年预计耗电
+ 耗材
+ 维护
+ 安装
- 预计残值
```

因此“便宜”不等于“性价比更高”。

---

# 10. Buy Agent

当用户已经基本确定商品：

```text
加入 Decision Watchlist
↓
Price Agent 持续检查
↓
价格进入目标区间
↓
提醒用户
↓
判断是否存在大促等待价值
↓
生成购买建议
```

例如：

> “现在 ¥2,699，距离你的目标价 ¥2,499 还有 7.4%。双11还有 18 天，且你当前不急用，我建议继续等。”

---

# 11. After Agent

购买后商品自动进入 Ownership。

管理：

- 物流；
- 收货；
- 退货期限；
- 价保期限；
- 发票；
- 保修；
- 安装；
- 使用手册；
- 故障；
- 维修。

例如：

> “这台耳机还有 3 天结束无理由退货。你之前两次提到右耳佩戴不舒服，如果问题还存在，建议现在决定是否退货。”

这才是 Memory 真正创造价值的地方。

---

# 12. Ownership Agent

用户最终形成自己的数字物品库：

```text
我拥有的设备
购买时间
价格
保修状态
使用周期
耗材
维修记录
当前二手价格
闲置程度
```

未来可以回答：

> “我家哪些家电今年会过保？”

> “去年数码产品一共花了多少钱？”

> “哪些东西很久没用了？”

> “这台电脑现在卖掉还是再用一年更划算？”

---

# 13. 商业模式

当前阶段：**不把盈利作为首要 KPI。**

商业化顺序：

### 第一阶段：免费私测

只验证：

> 用户在真实购买决策时会不会主动使用择适。

### 第二阶段：CPS / 联盟分佣

用户通过择适提供的推广链接完成交易，平台获得合规联盟佣金。

关键原则：

> **佣金不得进入推荐排序算法。**

系统甚至应记录：

```text
recommend_score
commission_rate
```

两者在推荐计算层彻底隔离。

### 第三阶段：高级能力

如果真实用户证明存在付费意愿，再考虑：

- 深度购买报告；
- 高级盯价；
- 更高分析额度；
- 家庭共享；
- 高级 Ownership。

不能一开始就假设用户愿意长期付月费。

---

# 14. AI Cost Control

这部分既是产品生存能力，也是 Java + Agent 工程学习重点。

## 14.1 Model Routing

请求进入统一 AI Gateway：

```text
Request
↓
Task Classifier
↓
Complexity Estimator
↓
Model Router
↓
Cheap / Mid / Strong Model
```

### Java / Rule Engine

不使用 LLM：

- 电流计算；
- 尺寸比较；
- 价格排序；
- 优惠计算；
- 条件过滤；
- 商品属性匹配。

### Small Model

- Intent；
- 参数抽取；
- 分类；
- 简单摘要。

### Mid Model

- 用户评价总结；
- 商品多维比较；
- 查询规划。

### Strong Model

只处理：

- 深度购买尽调；
- 多证据综合判断；
- 高难 Agent Planning。

---

## 14.2 Cost Budget

每个 Task 有预算：

```text
max_cost
max_input_tokens
max_output_tokens
max_model_calls
max_tool_calls
max_agent_steps
timeout
```

示例：

```text
RequirementExtraction
max_cost: ¥0.02

ReviewSummary
max_cost: ¥0.10

DeepPurchaseResearch
max_cost: ¥1.00
```

---

## 14.3 Infinite Loop Protection

必须实现：

```text
max_agent_steps = 8
max_model_calls = 6
max_tool_calls = 12
max_same_tool_repeat = 2
wall_clock_timeout = 90s
```

并加入：

- 重复计划检测；
- 相同 Tool 参数去重；
- Circuit Breaker；
- 失败快速退出；
- 降级模型 / 降级回答；
- Human fallback。

Agent 不能因为“没想明白”无限烧 Token。

---

# 15. Structured Intelligence Cache

商品研究结果不能每个用户重新分析。

例如：

```json
{
  "productId": "...",
  "knownIssues": [],
  "advantages": [],
  "commonComplaints": [],
  "suitableScenes": [],
  "unsuitableScenes": [],
  "evidenceVersion": "...",
  "lastUpdatedAt": "..."
}
```

第一次分析完成：

```text
Search
↓
RAG / LLM
↓
Product Intelligence
↓
MySQL / Search Index / Cache
```

第二个用户直接复用。

只有新增评价、新价格、新版本才增量更新。

这是 AI Cost Control 的核心能力之一。

---

# 16. Agent Observability

每一次 Agent Task 必须记录：

```text
task_id
user_id
model
prompt_version
input_tokens
output_tokens
latency
cost
tool_calls
steps
retry_count
final_status
confidence
```

最终后台至少能看到：

```text
今日 AI Task
成功率
平均延迟
平均成本
P95 成本
模型分布
Tool 失败率
循环熔断次数
```

学习重点：

> **不是“会调用模型”，而是“会运行一个受控、可观察、能算账的 AI 系统”。**

---

# 17. 产品合规原则

当前阶段优先私测。

如果未来公开服务，需要重新进行完整合规检查。

当前设计原则：

- 用户画像遵循最小必要；
- 偏好推断可查看、可修改、可删除；
- 不保存不必要敏感信息；
- 第三方商品和物流优先官方 API / 授权 API；
- 不绕验证码、不破解反爬；
- 正式公开 AI 功能时按届时中国大陆生成式 AI、APP/网站备案等规则处理；
- 商业化前确认联盟平台协议、税务和经营主体要求。

---

# 18. 经营主体路线

当前学习与私测：

> **不急于注册公司。**

如果出现：

```text
真实稳定用户
+
稳定联盟收入
+
需要签平台协议
+
需要支付 / 发票 / API合作
```

再决定：

```text
个体工商户
→ 验证商业模式

有限公司
→ 规模化 / 合作 / 招人 / 融资
```

作为普通公司员工，是否可以注册要结合劳动合同、保密和竞业约定检查。

择适绝不能使用现公司：

- 代码；
- 数据；
- 客户；
- 内部文档；
- 商业秘密；
- 非公开业务方案。

项目应从法律和职业伦理上保持独立。

---

# 19. 推广策略

产品验证阶段不投广告。

顺序：

```text
自己使用
↓
朋友 / 同事
↓
20~50 名种子用户
↓
真实购买案例
↓
可分享购买报告
↓
小红书 / 知乎 / B站 / 抖音内容
↓
邀请机制
↓
自然增长
```

内容本身可以成为增长入口：

> “700 元热水器到底应该看什么？”

> “第一次买路由器最容易踩的 5 个坑。”

> “AI 帮我发现我家根本不能装 7000W 热水器。”

只有证明：

```text
LTV > CAC
```

以后才考虑付费投放。

---

# 20. 0号验证阶段

第一批目标：

> 20~50 名种子用户  
> ≥100 次真实购买决策

观察：

```text
Activation
用户是否完成第一次决策？

Decision Completion
是否得到明确购买方案？

Discovery Value
AI 是否发现用户原本不知道的风险？

Decision Influence
结果是否影响真实购买？

Return Intent
下次买东西是否还想回来？

Referral
是否愿意推荐给朋友？
```

最关键的问题：

> **“下一次准备买东西时，你会先打开择适，还是先打开豆包 / 千问 / 淘宝 / 京东？”**

这比 DAU 更重要。

---

# 21. 项目学习目标：70%

本项目首先是一个完整 Java 后端 + AI Engineering 训练场。

最终目标技术地图：

```text
Java
Spring Boot
MySQL
Git
Maven
Linux

↓
Agent Runtime
LLM API
Structured Output
Tool Calling
Model Routing
Cost Budget

↓
Search
RAG
Recommendation
User Profile
Product Intelligence

↓
Redis
MQ
Event Driven
Scheduler
Idempotency
Retry

↓
Docker
Nginx
Jenkins / CI-CD
Logs
Metrics
JVM
Production Debugging

↓
真实用户
AI Cost
Performance
Security
Privacy

↓
必要时再：
Microservice
Gateway
Nacos
Sentinel
Distributed System
```

原则：

> **没有真实问题，不为了简历堆技术。**

---

# 22. 六个月开发排期

采用 **2 周一个 Sprint**。

每个 Sprint：

```text
需求
↓
设计
↓
开发
↓
测试
↓
README / ADR
↓
GitHub Push
↓
Code / Architecture Review
↓
验收
↓
下一 Sprint
```

---

## Sprint 1｜2026-09-15 ～ 2026-09-28

### 目标：工程真正跑起来

学习：

- Git；
- Maven；
- Spring Boot；
- REST；
- MySQL；
- 基础异常处理；
- 单元测试基础。

交付：

```text
zeshi-backend
```

包含：

- 用户；
- Session；
- 基础商品；
- Conversation；
- MySQL Migration；
- Swagger/OpenAPI；
- README。

验收：

- 可以 clone 后一条命令运行；
- 数据库可初始化；
- API 有统一返回与异常处理；
- Git commit 基本规范。

---

## Sprint 2｜2026-09-29 ～ 2026-10-12

### Consumer Profile + Requirement

加入：

- ConsumerPreferenceProfile；
- HomeProfile；
- Requirement Session；
- 用户画像修改；
- 基础前端/接口联调。

学习：

- 数据模型；
-事务；
-校验；
- DTO / Domain 分层。

---

## Sprint 3｜2026-10-13 ～ 2026-10-26

### AI Gateway V1

加入：

- LLM API；
- Structured Output；
- Prompt Version；
- Model Provider Interface；
- Model Routing V1；
- AI Task 表；
- Token / Cost 记录。

第一只 Agent：

> Requirement Agent

---

## Sprint 4｜2026-10-27 ～ 2026-11-09

### Search + Product Research

加入：

- Search Adapter；
- Product Canonical Model；
- Offer；
- Evidence；
- 商品链接 / 文本输入；
- Product Intelligence Cache V1。

学习：

- Adapter Pattern；
- External API；
- Rate Limit；
- Cache 思维。

---

## Sprint 5｜2026-11-10 ～ 2026-11-23

### Category Knowledge + RAG

加入：

- Category Schema；
- Knowledge Document；
- RAG；
- Constraint Rule；
- 至少 3 个类目：

```text
热水器
路由器
耳机
```

Agent 可以主动询问关键条件。

---

## Sprint 6｜2026-11-24 ～ 2026-12-07

### Decision Agent V1

完成：

```text
Requirement
→ Search
→ Evidence
→ Rule
→ Compare
→ Recommendation
```

输出第一版 Purchase Report。

加入：

- Recommendation Engine；
- 适配度；
- Evidence；
- Confidence。

目标：

> 第一批朋友可以真正使用。

---

## Sprint 7｜2026-12-08 ～ 2026-12-21

### Redis + Agent Cost Control

加入：

- Redis；
- Task Cache；
- Distributed Lock 基础；
- Cost Budget；
- Step Limit；
- Tool Limit；
- Circuit Breaker；
- Agent Loop Protection。

学习重点：

> 为什么需要 Redis，而不是“因为简历要 Redis”。

---

## Sprint 8｜2026-12-22 ～ 2027-01-04

### Price / Buy Agent

加入：

- Offer；
- Price History；
- Promotion；
- Target Price；
- Watchlist；
- Scheduler；
- 通知抽象。

开始学习异步任务。

---

## Sprint 9｜2027-01-05 ～ 2027-01-18

### Event Driven + MQ

加入：

- MQ；
- Domain Event；
- Retry；
- Idempotency；
- DLQ；
- PriceChanged；
- PurchaseCreated。

让技术需求自然推动 MQ。

---

## Sprint 10｜2027-01-19 ～ 2027-02-01

### AfterBuy / Ownership V0

加入：

- Purchase；
- OwnedItem；
- Warranty；
- ReturnWindow；
- Maintenance；
- Reminder。

把整个消费生命周期第一次串起来。

---

## Sprint 11｜2027-02-02 ～ 2027-02-15

### Production Engineering

学习与加入：

- Linux；
- Docker；
- Nginx；
- Jenkins / CI-CD；
- Logs；
- Metrics；
- JVM；
- Thread Dump；
- Heap；
- 故障模拟。

要求：

> Git Push → Build → Test → Deploy

完整跑通。

---

## Sprint 12｜2027-02-16 ～ 2027-03-01

### Seed User Beta

目标：

- 20+ 真实用户；
- 收集 ≥50 次购买决策；
- Feedback；
- Agent Cost Dashboard；
- Success Rate；
- Latency；
- Product Metrics。

完成：

> Zeshi Beta V0.1

并进行第一次完整技术复盘。

---

# 23. GitHub 验收协议

每一个 Sprint 完成后提交：

```text
1. GitHub Repo / PR
2. README 更新
3. 本 Sprint 功能说明
4. 架构变化
5. 数据库变化
6. API
7. 测试
8. 遇到的问题
9. 你自己的技术复盘
```

验收维度：

```text
功能正确性        20
代码设计          15
Java 基础          15
数据库             10
工程规范           10
测试               10
AI Engineering     10
问题理解            5
复盘                5
---------------------
总分               100
```

每次给出：

- Sprint 分数；
- 必须修复项；
- 推荐优化项；
- 技术追问；
- 下一阶段是否允许进入。

目标不是“让 AI 替你写完”。

目标是：

> **你必须能够解释每一段关键设计为什么存在。**

---

# 24. 项目成功标准

六个月以后，即使择适没有赚到一分钱，只要达到以下标准，项目仍然成功：

### Java

能独立：

- 搭服务；
- 设计数据库；
- 接外部 API；
- 用 Redis；
- 用 MQ；
- 部署 Linux；
- CI/CD；
- 定位 JVM / 服务问题。

### AI Engineering

能解释并实现：

- Agent Runtime；
- Tool Calling；
- Model Routing；
- RAG；
- Memory / Profile；
- Recommendation；
- Cost Budget；
- Loop Protection；
- Agent Observability。

### Product

有：

- 真实用户；
- 真实购买问题；
- 真实反馈；
- 产品迭代记录。

### Interview

能够说：

> “这个系统为什么这样设计？”

而不是：

> “因为教程就是这么写的。”

---

# 25. 商业成功标准

这是第二优先级。

先验证：

> 用户会不会使用。

再验证：

> 用户会不会回来。

再验证：

> 能不能形成交易。

最后才验证：

> 能不能盈利。

不能反过来。

---

# 26. 最终愿景

未来的择适不应该只是：

> “买东西时问一下 AI。”

而是：

> **一个真正了解我消费偏好、家庭环境、已有物品和长期需求的个人 Consumer Agent。**

它知道：

- 我已经拥有什么；
- 我重视什么；
- 什么东西适合我的环境；
- 什么价格对我来说值得；
- 什么东西根本没必要买；
- 什么东西适合买二手；
- 什么东西值得等；
- 买完以后什么时候退、修、换、卖。

最终我们希望用户产生一种感觉：

> **“以后买东西，我先问择适。”**

这就是产品成立的那一天。
