# Changelog

All notable dataset changes are documented here.

## 2.0.0 — 2026-07-14

- Converted the block-delimited TXT source to standards-compliant UTF-8 JSON Lines.
- Organized records by `layer` and `subcat`.
- Split categories into shards of at most 5,000 records.
- Added stable `record_id` and content-based `record_hash` fields.
- Added a JSON Schema, machine-readable manifest, statistics, checksums, sample records, data card, data dictionary, and quality report.
- Preserved all 214,119 source records, including exact duplicates and missing values.

## 1.0.0 — 2026-07-13

- Initial packaged release based on the updated source TXT and supplementary workbooks.
