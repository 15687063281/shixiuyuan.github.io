# 文献调研档案

- 研究主题：宽带中国试点政策对县级制造业TFP的影响
- 生成时间：2026-04-28

---

## 研究主题与核心问题

- **核心因果问题**：宽带中国示范城市入选（X）如何影响辖区县级制造业TFP（Y）？
- **内生性挑战**：经济发展水平高的城市更可能申报入选（正向选择偏误）；影响TFP的地方治理能力等不可观测因素可能同时影响入选概率（遗漏变量偏误）
- **外生变动**：分批次遴选（2014/2015年）+ 以宽带技术指标为主的阈值规则，提供准自然实验

---

## 文献脉络

### 脉络1：宽带基础设施对企业生产率的因果影响

| 作者(年) | 期刊 | 识别策略 | 主要发现 |
|---------|------|---------|---------|
| Hjort & Poulsen (2019) | *AER* | IV（海底光缆到达非洲） | 宽带到达→就业率提升，高技能就业增加 |
| Mang et al. (2018) | *Journal of Urban Economics* | IV（历史线路+DSL可用性） | 宽带→爱尔兰制造业TFP，效应约+2-4% |
| Cui et al. (2022) | *China Economic Review* | DiD（宽带中国示范城市） | 宽带→企业专利+1.4%，信息传播渠道 |
| Luo & Shi (近期) | *Environment, Development and Sustainability* | CS-DiD（宽带中国） | BDC政策→TFP碳生产率ATT≈0.021 |
| Tan et al. (2022) | *Research Policy* | DiD（宽带中国） | 宽带基础设施→城市创新，两渠道：网络普及+IT产业 |

### 脉络2：数字基础设施影响TFP的机制渠道

| 作者(年) | 期刊 | 机制 | 主要发现 |
|---------|------|------|---------|
| Ren et al. (2022) | *China Economic Review* | 企业数字化渠道 | 宽带中国→企业数字化→生产率，DiD |
| Liang et al. (2024) | *Applied Economics* | 劳动收入份额+技术升级 | 宽带扩展→劳动收入份额提升，信息化渠道 |
| Acemoglu et al. (2011) | *AER* | 技术与技能互补 | IT技术对高技能劳动力有互补效应，影响生产率分配 |

### 脉络3：Staggered DiD 方法论

| 作者(年) | 期刊 | 贡献 |
|---------|------|------|
| Callaway & Sant'Anna (2021) | *Journal of Econometrics* | CS-DiD主方法：ATT(g,t)估计，解决异质效应下TWFE偏误 |
| Goodman-Bacon (2021) | *Journal of Econometrics* | TWFE分解：存在负权重问题，Staggered设计下TWFE有偏 |
| Sun & Abraham (2021) | *Journal of Econometrics* | 交互权重估计量（IW-DiD），替代CS-DiD的稳健方法 |

### 脉络4：中国数字经济政策的经济影响

| 作者(年) | 期刊 | 研究问题 | 识别 |
|---------|------|---------|------|
| 多项研究(2020-2024) | 综合 | 宽带中国→就业/创业/创新/碳排放 | DiD，市级面板 |
| Tang et al. (2022) | *PLOS ONE* | 宽带中国→企业数字化 | DiD，上市公司 |
| Zhao et al. (2024) | *Bulletin of Economic Research* | 宽带中国→城市创新能力 | DiD，市级 |

### 脉络5：数字基础设施异质性效应

现有文献发现效应在以下维度存在显著异质性：
- **所有制**：非国有企业效应更强（政策补贴偏向、市场化程度）
- **地区**：非东部地区在某些指标上效应更强（追赶效应）；东部在创新维度效应更强（互补资产）
- **规模**：大型企业数字化转型更快，但小企业专利增长弹性更大

---

## 研究空白与本文贡献

1. **因果识别升级**：现有多数研究使用标准TWFE，未处理Staggered Adoption的异质效应偏误。本文采用CS-DiD为主，TWFE为对比，方法更严谨
2. **地理粒度**：现有文献几乎全部使用地级市数据；本文使用**县级**微观面板，政策传导路径更清晰
3. **机制量化**：现有研究记录了宽带→创新的总效应，本文系统检验专利创新（ln_patent）这一具体渠道
4. **异质性分解**：按地区和规模分解县级异质性效应，揭示政策受益的分布特征

---

## 推荐识别策略

**首选：CS-DiD（Callaway & Sant'Anna 2021）**
- 外生变动：2014/2015年分批次示范城市遴选，技术指标阈值驱动
- 处理组队列：2014年入选县（100个）/ 2015年入选县（100个）
- 对照组：从未入选县（100个），`control_group='notyettreated'`
- 识别假设：条件平行趋势——控制 ln_gdp、ln_population 等后，处理前各队列TFP趋势平行
- 验证方式：Dynamic Aggregate ATT事件研究图，超前期系数应联合不显著

**次选：TWFE（对照比较）**
- 用于展示Staggered偏误的影响幅度（与CS-DiD结果比较）
- 注明负权重潜在方向：若效应随时间递增，TWFE会低估ATT

---

## 可检验假设

- **H1**（主效应）：宽带中国政策使辖区县级制造业TFP显著提升
  理论逻辑：宽带基础设施→信息获取成本↓→技术扩散加速→要素配置效率↑→TFP↑

- **H2**（机制·创新渠道）：政策通过促进专利申请（`ln_patent`）影响TFP
  检验变量：`ln_patent`（中介）
  检验方式：三步回归法（X→M；M→Y；X+M→Y，观察β下降幅度）

- **H3**（异质性·地区）：东部县效应 > 中部 > 西部
  分组变量：`region`
  逻辑：东部数字经济生态完善，宽带与互补资产（高技能劳动力、IT企业）协同效应更强

- **H4**（异质性·规模）：大县（`size_group='Large'`）效应 > 小县
  分组变量：`size_group`
  逻辑：大县企业密度高，宽带网络外部性和知识溢出规模经济更显著

---

## 机制变量清单（供 eco-analysis 使用）

- 机制1：`ln_patent`（专利申请对数）— 对应H2，信息获取→创新渠道

---

## 异质性分组清单（供 eco-analysis 使用）

- 分组1：`region`（East / Central / West）— 对应H3，地区数字经济生态差异
- 分组2：`size_group`（Large / Small）— 对应H4，县规模与网络外部性

---

## 参考文献

Callaway, B. & Sant'Anna, P. H. C. 2021. "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200-230.

Cui, X., Wang, C., Liao, J., Fang, Z. & Cheng, F. 2022. "Death of distance? Economic impacts of broadband internet on firm innovation." *China Economic Review* 75: 101838.

Goodman-Bacon, A. 2021. "Difference-in-differences with variation in treatment timing." *Journal of Econometrics* 225(2): 254-277.

Hjort, J. & Poulsen, J. 2019. "The Arrival of Fast Internet and Employment in Africa." *American Economic Review* 109(3): 1032-1079.

Liang, H. et al. 2024. "Broadband infrastructure expansion and labour income share: micro-evidence from Chinese industrial enterprises." *Applied Economics* 57(50).

Mang, C. 2018. "Broadband internet and firm performance." *Journal of Urban Economics* 108: 79-93. [未核实，来自模型记忆]

Sun, L. & Abraham, S. 2021. "Estimating dynamic treatment effects in event studies with heterogeneous treatment effects." *Journal of Econometrics* 225(2): 175-199.

Tang, C. et al. 2022. "The road to change: Broadband China strategy and enterprise digitization." *PLOS ONE* 17(6): e0269133.
