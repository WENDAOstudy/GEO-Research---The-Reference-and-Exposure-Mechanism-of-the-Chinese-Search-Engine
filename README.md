# AIDSO Results Dataset v2

本仓库用于发布 AIDSO 结果数据及其更新明细。仓库仅包含数据与配套文档，不包含程序代码。

## 文件结构

```text
.
├── README.md
├── SHA256SUMS.txt
├── .gitattributes
├── .gitignore
├── data/
│   ├── raw/
│   │   └── aidso-results-v2-updated.zip
│   └── updates/
│       └── answer-level-1-updated.xlsx
└── docs/
    ├── field-dictionary.xlsx
    └── publishing-checklist.md
```

## 数据文件

| 文件 | 格式 | 记录数 | `prompt_id` 数量 | 说明 |
|---|---:|---:|---:|---|
| `data/raw/aidso-results-v2-updated.zip` | ZIP（内含 UTF-8 文本） | 214,119 | 610 | 完整结果明细；按 `prompt_id` 替换更新内容后的主文件 |
| `data/updates/answer-level-1-updated.xlsx` | XLSX | 15,771 | 40 | 40 个更新问题的引用/检索结果明细 |
| `docs/field-dictionary.xlsx` | XLSX | — | — | 文件概览、字段定义和使用建议 |

## 主文件格式

解压 `aidso-results-v2-updated.zip` 后可得到 `aidso-results-v2-updated.txt`。文本保留原始 UTF-8 格式。每个记录块包含一条引用或检索结果明细，记录块之间使用两个空行分隔。

请注意：`snippet` 等长文本字段中可能包含单个换行，因此不能简单地按“一行一条记录”读取。读取时应以两个空行为记录边界，并保留记录块内部的换行。

## 字段

两个数据文件使用同一套 12 个字段：

| 字段 | 含义 |
|---|---|
| `prompt` | 原始问题文本 |
| `platform_code` | 平台、渠道或模型代码 |
| `quote_url` | 引用网址 |
| `quote_title` | 引用标题 |
| `site_name` | 来源网站、应用或平台名称 |
| `quote_index` | 当前回答或检索结果中的引用序号 |
| `published_at` | 来源内容的发布日期或时间 |
| `domain` | 来源域名 |
| `snippet` | 引用正文、摘要或检索片段 |
| `prompt_id` | 问题分组标识；不是行级唯一键 |
| `layer` | 一级分类 |
| `subcat` | 二级分类 |

更完整的类型、空值规则、示例和注意事项见 `docs/field-dictionary.xlsx`。

## 数据使用注意事项

- 同一个 `prompt_id` 通常对应多个平台和多条引用记录，不能将其视为行级唯一键。
- `quote_url`、`published_at`、`domain` 和 `snippet` 等字段允许为空。
- 日期字段可能为空或格式不统一，分析前应先标准化。
- 去重时应根据具体用途组合使用 `prompt_id`、`platform_code`、`quote_url` 和 `quote_index`。
- `SHA256SUMS.txt` 提供文件校验值，可用于检查下载或移动后文件是否完整。

## 数据下载

主数据以 ZIP 压缩包形式存储，可通过普通 Git 克隆或从 GitHub 仓库页面直接下载。解压后请使用 `SHA256SUMS.txt` 中提供的压缩包校验值核对文件完整性。

## 许可证与权利说明

本数据集尚未指定开放数据许可证。数据中包含第三方网页标题、链接和正文片段；公开发布前，请确认数据采集、存储和再分发符合来源网站条款、著作权要求及适用的数据保护规则。完成权属确认后，再选择适合的数据许可证，并在仓库根目录添加 `LICENSE` 文件。

## 版本

- 数据版本：v2 updated
- 文档整理日期：2026-07-13
