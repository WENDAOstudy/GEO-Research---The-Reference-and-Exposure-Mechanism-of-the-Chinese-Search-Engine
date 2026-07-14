# CN-GEO 引用数据集

[![记录数](https://img.shields.io/badge/records-214%2C119-2563eb)](data/statistics.json)
[![格式](https://img.shields.io/badge/format-JSONL-0f766e)](schema/record.schema.json)
[![版本](https://img.shields.io/badge/version-2.0.0-7c3aed)](CHANGELOG.md)
[![许可](https://img.shields.io/badge/license-CC%20BY%204.0-d97706)](LICENSE.md)

**面向中文生成式搜索平台引用选择与来源曝光研究的结构化数据集。**

[English](README.md) · [简体中文](README.zh-CN.md)

## 数据集简介

CN-GEO 引用数据集收录了基准问题在 12 个平台代码下产生的引用与检索结果。此版本将原始记录块文本完整转换为 UTF-8 JSON Lines，按照研究维度与子类别组织，并提供 schema、manifest、校验值、数据卡和质量报告。

| 指标 | 数值 |
|---|---:|
| 引用记录 | 214,119 |
| 非空问题 ID | 609 |
| 平台代码 | 12 |
| 一级研究维度 | 7 |
| 维度/子类别组合 | 32 |
| JSONL 分片 | 64 |
| 最大分片 | 7.31 MiB |

## 仓库结构

```text
.
├── README.md / README.zh-CN.md
├── CITATION.cff
├── CHANGELOG.md
├── CHECKSUMS.sha256
├── LICENSE.md
├── data/
│   ├── manifest.json
│   ├── statistics.json
│   ├── README.md
│   └── records/<维度>/<子类别>/part-*.jsonl
├── docs/
│   ├── DATA_CARD.md
│   ├── DATA_DICTIONARY.md
│   └── QUALITY_REPORT.md
├── examples/sample.jsonl
└── schema/record.schema.json
```

## 分类组织

数据按 `layer` 和 `subcat` 分组，每个文件最多 5,000 条记录，同一分类内部保留源文件顺序。

| 一级分类 | 目录名 | 记录数 |
|---|---|---:|
| 极端与真实场景 | `edge-real-world` | 68,089 |
| 提问属性 | `query-intent` | 51,201 |
| 行业维度 | `industry` | 37,528 |
| 提示风格 | `prompt-style` | 19,996 |
| 时间敏感度 | `time-sensitivity` | 18,653 |
| 触发强度 | `trigger-intensity` | 14,219 |
| 未分类 | `uncategorized` | 4,433 |

完整的分类映射、文件路径、记录数、文件大小和 SHA-256 见 [`data/manifest.json`](data/manifest.json)。

## 数据格式

每行是一个独立 JSON 对象，并符合 [`schema/record.schema.json`](schema/record.schema.json)。在 12 个源字段之外，新版增加：

- `record_id`：按源文件顺序生成的稳定记录标识。
- `record_hash`：标准化后 12 个源字段的 SHA-256 内容哈希。

字段含义见 [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md)，示例见 [`examples/sample.jsonl`](examples/sample.jsonl)。

## 使用示例

```python
import json
from pathlib import Path

for path in Path("data/records").rglob("*.jsonl"):
    with path.open(encoding="utf-8") as stream:
        for line in stream:
            record = json.loads(line)
```

## 数据质量

214,119 条源记录全部解析成功。为保持原始研究总体口径，完全重复记录未被删除。缺失值、URL 检查、重复记录和已知限制见 [`docs/QUALITY_REPORT.md`](docs/QUALITY_REPORT.md)。

## 引用

建议引用：

> WENDAOstudy. *CN-GEO Citation Dataset*. Version 2.0.0, 2026.

机器可读引用信息见 [`CITATION.cff`](CITATION.cff)。

## 许可与责任

数据集结构、标注和文档采用 [CC BY 4.0](LICENSE.md)。其中的第三方网页标题、URL 和内容片段可能仍受原发布者权利约束；使用者应自行遵守相关网站条款、著作权、隐私保护与研究伦理要求。

## 项目地址

`https://github.com/WENDAOstudy/cn-geo-citation-dataset`
