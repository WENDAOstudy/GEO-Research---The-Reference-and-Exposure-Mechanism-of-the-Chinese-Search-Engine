# Data access guide

The canonical release is stored as UTF-8 JSON Lines under `data/records/`.

## Partitioning

```text
data/records/<layer-slug>/<subcat-slug>/part-0001.jsonl
```

- Records are grouped by the source `layer` and `subcat` fields.
- Each shard contains at most 5,000 records.
- Source order is preserved within each category.
- A record never spans multiple physical lines; embedded text newlines are JSON-escaped.

Use `manifest.json` for programmatic discovery instead of hard-coding paths. It contains the category mapping, record counts, byte sizes, and SHA-256 checksum of every shard.

The source TXT and intermediate spreadsheets are not duplicated in this repository. Their provenance and source checksum are recorded in `manifest.json`.
