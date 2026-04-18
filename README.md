# 中文文档标点规范 Skill

这是一个 Codex 全局 skill，用于规范中文正式文档中的标点、空格和明确上下角标。适合处理计划书、方案书、报告、论文、学位论文、期刊稿、公文和中英文混排文本。

## 功能

- 统一中文正文中的全角标点和中英文混排空格。
- 删除中文与英文、中文与数字之间不必要的空格。
- 保留英文短语、产品名、技术表达内部的英文空格。
- 规范明确的上下角标，例如化学式、离子价态、数学次方、平方/立方单位。
- 处理论文时保护参考文献、引用标、脚注、尾注和作者-年份引用。
- 在上下角标判断不确定时，支持条件联网核查权威来源，而不是直接猜测。

## 关键规则

中文正文采用正式文档风格：

- `本项目采用 AI 技术。` -> `本项目采用AI技术。`
- `周期为 3 个月。` -> `周期为3个月。`
- `本项目采用AI, 大数据和云计算技术。` -> `本项目采用AI、大数据和云计算技术。`

明确上下角标采用保守处理：

- `H2O` -> `H₂O`
- `CO2` -> `CO₂`
- `Na2SO4` -> `Na₂SO₄`
- `Ca(OH)2` -> `Ca(OH)₂`
- `NH4+` -> `NH₄⁺`
- `SO4^2-` -> `SO₄²⁻`
- `10^6` -> `10⁶`
- `20 m2` -> `20 m²`

默认不改这些内容：

- `参考文献`、`References`、`Bibliography`、`Works Cited` 后的参考文献条目。
- `[1]`、`[1-3]`、`［1］`、上标引用号、脚注号、尾注号。
- URL、代码、路径、版本号、型号、产品名、文档编号。
- `H2AX`、`p53`、`C2C12`、`IL-6` 等基因、蛋白、细胞系或生物医学标识符。

## 条件联网核查

当某个表达可能是化学式、基因名、材料型号、产品型号或复杂单位时，skill 会优先保留原样；只有在高价值且可由权威来源确认时，才建议联网核查。

优先来源：

- 化合物和化学式：PubChem、NIST Chemistry WebBook、IUPAC、权威期刊或教材。
- 单位和 SI 记法：BIPM/SI、NIST、ISO 或国家标准。
- 论文格式：目标期刊、会议、出版社或学校论文格式指南。

## 安装

将仓库中的 `standardize-chinese-document-punctuation` 文件夹复制到 Codex 的全局 skills 目录：

```powershell
Copy-Item -Recurse -Force .\standardize-chinese-document-punctuation "$env:USERPROFILE\.codex\skills\standardize-chinese-document-punctuation"
```

安装后，重启 Codex 或刷新 skill 列表即可使用。

## 文件结构

```text
standardize-chinese-document-punctuation/
├── README.md
└── standardize-chinese-document-punctuation/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## 使用示例

可以这样请求 Codex：

```text
请按中文正式文档规范整理这份计划书正文的标点、空格和明确上下角标。
```

```text
请处理这篇论文正文中的中英文空格、标点和明确化学式上下标，但不要修改参考文献和引用标。
```
