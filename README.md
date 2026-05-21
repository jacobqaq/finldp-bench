# FinLDP-Bench Dataset

The **FinLDP-Bench (Financial Logic-Driven Document Generation Benchmark)** dataset is a benchmark designed to evaluate financial document generation systems under the **Logic-Driven Document Generation Problem (LDP)** setting. In LDP, a system must generate a complete domain-specific report that is not only factually grounded, but also consistent with the writing logic and data usage patterns of sample reports from a specific institution.

---

## Overview

FinLDP-Bench focuses on financial analyst report generation, where each sample is organized as a structured record with predefined fields. The dataset covers five representative financial verticals:

| Subset | #Files | #Samples | Domain | Institution |
|---|---:|---:|---|---|
| **Agriculture** | 10,000 | 30,000 | Agriculture research reports | Pacific Securities Co., Ltd. |
| **Cotton** | 10,000 | 30,000 | Cotton futures research reports | CMB Futures Co., Ltd. |
| **ETF** | 10,000 | 30,000 | ETF weekly reports | Maigao Securities Co., Ltd. |
| **Macro** | 10,000 | 30,000 | Macro research reports | Ping An Securities Co., Ltd. |
| **Precious Metals** | 10,000 | 30,000 | Precious metals research reports | Soochow Securities Co., Ltd. |

Each `case_*.csv` file contains multiple reports from the same vertical. These reports can be used as sample documents for learning reusable writing logic and as references for evaluating generated reports.

---

## Dataset Structure

The dataset is organized by financial vertical:

```text
FinLDP-Bench/
├── Agriculture/
│   └── data/
│       ├── case_1.csv
│       ├── case_2.csv
│       └── ...
├── Cotton/
│   └── data/
├── ETF/
│   └── data/
├── Macro/
│   └── data/
└── Precious_Metals/
    └── data/
```

---

## Data Format

Each CSV file is encoded in UTF-8 and contains structured report records. The first column is usually `report_id`, and the remaining columns correspond to predefined report fields.

Example:

```csv
report_id,市场回顾,行业信息,风险提示
20170904,...,...,...
20180309,...,...,...
```

Different subsets may use different field names because financial institutions follow different writing conventions and report templates. This design allows FinLDP-Bench to evaluate whether a generation system can adapt to institution-specific writing logic.

---

## Task Setting

Given:

- a user query specifying the target report type and reference date,
- several sample reports from the same subset,
- and external financial data sources,

the goal is to generate a complete report that satisfies:

1. **Logic consistency**: the generated report should follow the writing paradigm of the sample reports.
2. **Data sufficiency**: the generated report should cover the required data types and key facts.
3. **Data accuracy**: numerical values and reference dates should be consistent with reliable data sources and the user query.

---

## Usage

For the LogicRAG implementation, each `case_*.csv` file can be passed to the document learner. For example:

```powershell
python document_learner.py `
  --csv "dataset\Precious_Metals\data\case_2253.csv" `
  --row-a 0 `
  --row-b 1 `
  --output-dir "logicrag_outputs"
```

The selected rows are treated as sample reports for extracting reusable writing logic.

---

## Citation

If you use FinLDP-Bench in your research, please cite:

```bibtex
@article{logicrag2026,
  title={LogicRAG: A Logic-Driven Framework for Financial Document Generation with Retrieval-Augmented Generation},
  author={Anonymous},
  year={2026}
}
```
