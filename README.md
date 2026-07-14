# CN-GEO Citation Dataset

[![Records](https://img.shields.io/badge/records-214%2C119-2563eb)](data/statistics.json)
[![Format](https://img.shields.io/badge/format-JSONL-0f766e)](schema/record.schema.json)
[![Version](https://img.shields.io/badge/version-2.0.0-7c3aed)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-CC%20BY%204.0-d97706)](LICENSE.md)

**A structured citation corpus for studying reference selection and source exposure across Chinese generative search platforms.**

[English](README.md) · [简体中文](README.zh-CN.md)

## Overview

CN-GEO Citation Dataset contains citation and retrieval-result records associated with benchmark prompts across 12 platform codes. The release converts the original block-delimited text into standards-compliant UTF-8 JSON Lines, organizes records by research dimension and subcategory, and provides reproducible metadata, validation rules, checksums, and quality notes.

### At a glance

| Metric | Value |
|---|---:|
| Citation records | 214,119 |
| Non-null prompt IDs | 609 |
| Platform codes | 12 |
| Top-level dimensions | 7 |
| Dimension/subcategory pairs | 32 |
| JSONL shards | 64 |
| Largest shard | 7.31 MiB |

## Repository layout

```text
.
├── README.md                    # English landing page
├── README.zh-CN.md              # Chinese landing page
├── CITATION.cff                 # Citation metadata
├── CHANGELOG.md                 # Release history
├── CHECKSUMS.sha256             # Integrity checks
├── LICENSE.md                   # Dataset license and third-party notice
├── data/
│   ├── manifest.json            # Machine-readable file index
│   ├── statistics.json          # Dataset-level statistics
│   ├── README.md                # Data access guide
│   └── records/
│       └── <dimension>/<subcategory>/part-*.jsonl
├── docs/
│   ├── DATA_CARD.md
│   ├── DATA_DICTIONARY.md
│   └── QUALITY_REPORT.md
├── examples/sample.jsonl
└── schema/record.schema.json
```

## Data organization

Records are grouped by `layer` and `subcat`. Each category is split into shards of at most 5,000 records, preserving source order within that category.

| Dimension (`layer`) | Directory | Records |
|---|---|---:|
| 极端与真实场景 | `edge-real-world` | 68,089 |
| 提问属性 | `query-intent` | 51,201 |
| 行业维度 | `industry` | 37,528 |
| 提示风格 | `prompt-style` | 19,996 |
| 时间敏感度 | `time-sensitivity` | 18,653 |
| 触发强度 | `trigger-intensity` | 14,219 |
| 未分类 | `uncategorized` | 4,433 |

The complete category-to-file mapping, record counts, byte sizes, and SHA-256 hashes are available in [`data/manifest.json`](data/manifest.json).

## Record format

Each line is an independent JSON object validated against [`schema/record.schema.json`](schema/record.schema.json). The release preserves the 12 source fields and adds two derived fields:

- `record_id`: stable source-order identifier, such as `cngeo-000000001`.
- `record_hash`: SHA-256 hash of the normalized 12-field source record.

See [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md) for field definitions and [`examples/sample.jsonl`](examples/sample.jsonl) for examples.

## Quick start

```python
import json
from pathlib import Path

for path in Path("data/records").rglob("*.jsonl"):
    with path.open(encoding="utf-8") as stream:
        for line in stream:
            record = json.loads(line)
```

## Data quality

All 214,119 source records were parsed successfully. Exact duplicates are retained to preserve the original research population. Missing values, URL diagnostics, duplicate counts, and known limitations are documented in [`docs/QUALITY_REPORT.md`](docs/QUALITY_REPORT.md).

## Citation

If you use this dataset, cite the repository metadata in [`CITATION.cff`](CITATION.cff):

> WENDAOstudy. *CN-GEO Citation Dataset*. Version 2.0.0, 2026.

## License and responsible use

The dataset structure, annotations, and documentation are released under [CC BY 4.0](LICENSE.md). Quoted titles, URLs, and excerpts may remain subject to their original publishers' rights. Users are responsible for complying with applicable terms, copyright requirements, privacy rules, and research-ethics standards.

## Project URL

`https://github.com/WENDAOstudy/cn-geo-citation-dataset`
