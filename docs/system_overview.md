# Auto-Eco 系统逻辑总览

最后更新：2026-05-02

Auto-Eco 是一个面向计量经济学论文的自动科研流水线。系统目标不是只生成一份报告，而是围绕一个研究主题和数据集，循环完成数据探索、政策背景、文献调研、实证分析、论文写作、PDF 编译、Stata 复现代码和最终交付包。

## 核心原则

1. 目标驱动：每个阶段必须有明确产物和通过条件。
2. 循环迭代：阶段失败时进入 `needs_revision`，回到当前阶段或上游阶段修订。
3. 可复查：所有中间判断写入 `ECO_*`、`TODO` 和 `QA` 文件。
4. 不造事实：政策、文献、系数和表格必须来自可追踪来源或状态文件。
5. 可复现：最终必须产出 `analysis.do`，用于 Stata 复现主要实证结果。
6. 可交付：最终产物统一放入 `final_package/`。

## 总体流程

```text
输入：研究主题 + 数据路径
  |
  v
阶段0 研究问题发现（可选）
  -> ECO_IDEA.md
  |
阶段1 初始化研究简报
  -> ECO_BRIEF.md
  |
阶段2 数据探索
  -> ECO_DATA_PROFILE.md
  |
阶段2.5 研究切口关卡
  -> ECO_PIPELINE_QA.md
  |
阶段2.7 政策制度背景
  -> ECO_BACKGROUND.md
  |
阶段3 文献调研
  -> ECO_LIT.md
  |
阶段3.5 引用核查
  -> ECO_REFS_VERIFIED.md
  |
阶段4 实证分析
  -> ECO_RESULTS.md
  -> ECO_ANALYSIS_TODO.md
  -> ECO_ANALYSIS_QA.md
  -> tables/
  -> analysis.do
  |
阶段4.5 贡献声明
  -> ECO_CONTRIBUTION.md
  |
阶段5 论文写作
  -> ECO_WRITING_TODO.md
  -> ECO_SECTION_PLAN.md
  -> sections/
  -> ECO_WRITING_QA.md
  -> ECO_PAPER_DRAFT.md
  -> paper.tex
  -> paper.pdf
  |
最终打包
  -> final_package/
```

## 全局循环控制

`eco-pipeline` 必须维护两个全局文件：

```text
ECO_PIPELINE_TODO.md
ECO_PIPELINE_QA.md
```

阶段状态只能是：

```text
pending -> running -> needs_revision -> passed -> blocked
```

规则：

- 每个阶段开始前标记为 `running`。
- 每个阶段结束后立刻质检。
- 未达标时回到当前阶段或上游依赖阶段。
- 每阶段最多 3 轮修订。
- 有未处理的 `blocked` 或 `needs_revision` 时，不能输出完成。

## 数据与研究设计

`eco-data-explore` 负责识别：

- 数据文件格式和样本规模
- 个体 ID 和时间变量
- 候选被解释变量 Y
- 候选解释变量 X
- 控制变量
- 处理变量、政策年份、处理组和对照组
- 初步识别策略：DiD、IV、RDD、TWFE 等

`eco-pipeline` 的 2.5 阶段会检查研究切口是否足够具体：

1. 是否有具体政策或事件冲击。
2. 是否有明确冲击年份。
3. 是否有明确处理单元。
4. 是否有自然对照组。

低于门槛时，必须调整研究问题，不能硬进入实证分析。

## 政策背景与文献

`eco-background` 负责收集政策制度背景。政策事实必须来自权威来源或明确标记为待核查。

`eco-lit-review` 负责形成：

- 文献流
- 研究空白
- 理论机制
- 可检验假说
- 机制变量
- 异质性分组

`eco-ref-verify` 负责核查引用真实性。`FAIL` 引用不得进入最终论文。

## 实证分析循环

`eco-analysis` 必须输出：

```text
ECO_ANALYSIS_TODO.md
ECO_ANALYSIS_QA.md
ECO_RESULTS.md
tables/
analysis.do
```

分析模块包括：

1. 状态读取与识别设计
2. 数据清洗与样本诊断
3. 描述统计和平衡性
4. 基准回归
5. 动态效应或识别有效性
6. 稳健性检验
7. 机制检验
8. 异质性分析
9. Stata 复现代码
10. 结果归档与数字一致性

主结果不显著或方向相反时，不能自动换变量、换样本或换模型做 specification searching。必须先检查数据定义、模型设定、样本范围和识别假设；确认无误后如实记录结果。

## Stata 复现代码

最终必须生成：

```text
analysis.do
```

`analysis.do` 至少包括：

- 项目路径和日志
- 依赖检查：`reghdfe`、`estout`、`winsor2`、`csdid` 等
- 数据读取
- 变量定义
- 样本清洗
- 描述统计
- 基准回归
- 动态效应
- 稳健性
- 机制和异质性
- 表格导出

如果 Python/R 估计器无法被 Stata 完全等价复现，必须在 do-file 注释和 `ECO_ANALYSIS_QA.md` 中说明差异。

## 中文论文写作规则

`eco-write-paper` 默认采用国内经管类/CSSCI 风格。

硬性要求：

- 正文中文字符不少于 10,000 字。
- 统计时排除摘要、表图、公式、参考文献和附录。
- 低于 10,000 字不得生成最终版。
- 中文一级标题使用“一、二、三”。
- 二级标题使用“（一）（二）（三）”。
- 首页包含摘要、关键词、中图分类号、文献标识码、文章编号、DOI、收稿日期、基金项目和作者简介。
- 参考文献编号使用 `[1]`、`[2]`。

表格规则：

- 主文表格使用统一字号三线表。
- 不得对不同表格使用不同缩放比例。
- 英文变量名必须有中文解释。
- 回归系数必须带 `*`、`**`、`***` 显著性星号。
- 表下注明显著性水平、变量说明、固定效应和聚类层级。

## 最终交付包

流水线完成后必须生成：

```text
final_package/
  paper/
    paper.pdf
    paper.tex
    ECO_PAPER_DRAFT.md
  code/
    analysis.do
    analysis.log
  tables/
    table*.csv
    table*.txt
    figure*.pdf
    figure*.png
  docs/
    ECO_BRIEF.md
    ECO_DATA_PROFILE.md
    ECO_BACKGROUND.md
    ECO_LIT.md
    ECO_REFS_VERIFIED.md
    ECO_RESULTS.md
    ECO_CONTRIBUTION.md
  qa/
    ECO_PIPELINE_TODO.md
    ECO_PIPELINE_QA.md
    ECO_ANALYSIS_TODO.md
    ECO_ANALYSIS_QA.md
    ECO_WRITING_TODO.md
    ECO_SECTION_PLAN.md
    ECO_WRITING_QA.md
    WORD_COUNT_CHECK.md
  README.md
```

核心文件缺失时，不能标记为完整交付包：

- `paper/paper.pdf`
- `paper/paper.tex`
- `paper/ECO_PAPER_DRAFT.md`
- `code/analysis.do`
- `docs/ECO_RESULTS.md`
- `tables/`
- `qa/`
- `README.md`

## 当前 Demo

当前 demo 位于：

```text
demo_eco/final_package/
```

核心产物：

- PDF：`demo_eco/final_package/paper/paper.pdf`
- LaTeX：`demo_eco/final_package/paper/paper.tex`
- Stata：`demo_eco/final_package/code/analysis.do`
- 表图：`demo_eco/final_package/tables/`
- 质检：`demo_eco/final_package/qa/`

当前 demo 正文中文字符数超过 10,000 字，PDF 已编译成功。
