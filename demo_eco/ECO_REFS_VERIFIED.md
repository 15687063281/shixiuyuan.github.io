# 引用核查报告

- 项目目录：C:\demo_eco
- ECO_LIT.md 生成时间：2026-04-28
- 核查时间：2026-04-28
- 核查总数：8 条
- 通过：5 ✅ | 警告：2 ⚠ | 失败：1 ❌

---

## 核查结果

### ✅ 通过（5 条）

| # | 原始引用 | 核查来源URL | 备注 |
|---|---------|-----------|------|
| 1 | Callaway & Sant'Anna (2021) *Journal of Econometrics* 225(2):200-230 | https://www.sciencedirect.com/science/article/abs/pii/S0304407620303948 | 卷期页码精确匹配 |
| 2 | Goodman-Bacon (2021) *Journal of Econometrics* 225(2):254-277 | https://www.sciencedirect.com/science/article/abs/pii/S0304407621001445 | 标题、卷期页码精确匹配 |
| 3 | Hjort & Poulsen (2019) *AER* 109(3):1032-1079 | https://www.aeaweb.org/articles?id=10.1257/aer.20161385 | AEAweb官网精确匹配 |
| 4 | Liang et al. (2024) *Applied Economics* | https://www.tandfonline.com/doi/full/10.1080/00036846.2024.2399167 | Tandfonline精确匹配 |
| 5 | Sun & Abraham (2021) *Journal of Econometrics* 225(2):175-199 | https://www.sciencedirect.com/science/article/abs/pii/S030440762030378X | 卷期页码精确匹配 |

### ⚠ 警告（2 条，建议人工确认）

| # | 原始引用 | 疑问点 | 建议操作 |
|---|---------|--------|---------|
| 1 | Cui et al. (2022) "Death of distance?" *China Economic Review* | 找到同刊2022年宽带→企业创新论文，但标题为"Broadband internet and enterprise innovation"，且原文注明使用IV（电信改革），非DiD。作者首字母未核实 | Google Scholar搜索"Cui broadband enterprise innovation China Economic Review 2022"确认完整作者名和标题 |
| 2 | Tang et al. (2022) *PLOS ONE* 17(6):e0269133 | DOI存在（PLOS ONE官网有该文），但原文作者为Wang C & Zhang M，非"Tang et al."；期刊期号应为17(**5**)，非17(6) | 修正作者为Wang & Zhang，期号改为17(5):e0269133 |

### ❌ 失败（1 条，建议删除或替换）

| # | 原始引用 | 搜索过程 | 处置建议 |
|---|---------|---------|---------|
| 1 | Mang, C. 2018. "Broadband internet and firm performance." *Journal of Urban Economics* 108: 79-93. | 3次搜索均未在JUE找到该文。找到"Broadband upgrade and firm performance in rural areas" (Regional Science and Urban Economics)，但期刊/年份/标题不符 | **立即删除**。已标注[未核实，来自模型记忆]；可用已核实的Mang相关文献或下列替代文献替换 |

---

## 操作建议

### 立即删除
- R6：Mang (2018) *Journal of Urban Economics* — 假引用，删除

### 人工核查（Google Scholar）
1. **R2 Cui et al.（⚠）**：搜索 `Cui "broadband internet" "enterprise innovation" "China Economic Review" 2022`，确认作者全名和标题
2. **R8 Tang/Wang et al.（⚠）**：修正作者为 Wang, C. & Zhang, M.，期号由 17(6) 改为 17(5)

### 可用替代文献（替换 R6 假引用）
以下均为本次搜索中发现的真实文献，与原引用位置的论证目的（宽带→企业绩效）相符：

- **Battisti & Stoneman (2005)**，"The Intra-Firm Diffusion of New Process Technologies"，可参考技术扩散机制
- **Akerman, Gaarder & Mogstad (2015)**，"The Skill Complementarity of Broadband Internet"，*QJE*，NBER w20826 — ✅已核实，顶刊，宽带×技能互补→企业生产率
- **Chen (2020)**，"Broadband Internet, Firm Performance, and Worker Welfare"，*Economic Inquiry*，已发现Wiley在线链接 — 可搜索确认替换
