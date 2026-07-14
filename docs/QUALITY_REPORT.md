# Quality report

## Validation result

All **214,119** source records were parsed and serialized successfully. Every output line is valid JSON, every record contains the schema's required keys, and the largest shard is **7.31 MiB**.

## Duplicate records

There are **24,274 exact duplicate occurrences** beyond the first occurrence of each normalized record hash (**11.34%** of all rows). They are retained because repeated results may be analytically meaningful and removing them would change the original population.

## Missing values

| Field | Missing | Share |
|---|---:|---:|
| `published_at` | 74,509 | 34.80% |
| `snippet` | 7,816 | 3.65% |
| `prompt_id` | 4,433 | 2.07% |
| `site_name` | 3,573 | 1.67% |
| `quote_index` | 3,545 | 1.66% |
| `domain` | 2,802 | 1.31% |
| `quote_title` | 1,981 | 0.93% |
| `quote_url` | 1,133 | 0.53% |

## URL diagnostics

- 211,248 values are syntactically valid HTTP(S) URLs.
- 1,738 non-empty values do not match a strict HTTP(S) URL pattern.
- 1,133 values are empty.

Non-HTTP values are retained because some may represent application pages, mini-program identifiers, or platform-specific source references rather than data errors.

## Mixed-type citation positions

`quote_index` contains 205,780 integers, 4,794 platform-specific composite strings (for example `web_search:1#0`), and 3,545 null values. Composite strings are preserved rather than coerced because they encode platform-specific search-result positions.

## Known limitations

- Platform codes are opaque business identifiers; no authoritative public mapping is included.
- `published_at` is incomplete and may contain heterogeneous formats.
- Source snippets can be truncated, duplicated, promotional, or no longer available at the recorded URL.
- Categories reflect the supplied taxonomy and are not independently re-labeled.
- The source material does not document a complete collection methodology or sampling frame.

## Recommended analytical practice

- Report whether analyses are row-weighted, prompt-weighted, or deduplicated.
- Use `prompt_id + platform_code` when comparing platforms by question.
- Treat `record_hash` deduplication as a derived analytical choice.
- Keep the canonical release unchanged and write cleaned dates or domain mappings to separate derived files.
