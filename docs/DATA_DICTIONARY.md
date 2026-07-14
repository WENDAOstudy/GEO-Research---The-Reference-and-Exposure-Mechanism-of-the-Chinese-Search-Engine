# Data dictionary

| Field | Type | Nullable | Description |
|---|---|---:|---|
| `record_id` | string | No | Stable source-order ID in the form `cngeo-#########`. |
| `prompt` | string | No | Original benchmark question submitted to a platform or model. |
| `platform_code` | string | No | Business/platform code associated with the result. |
| `quote_url` | string | Yes | Source URL or source identifier returned with the result. |
| `quote_title` | string | Yes | Title of the cited page, document, application, or source. |
| `site_name` | string | Yes | Display name of the source site, app, mini program, or platform. |
| `quote_index` | integer/string/null | Yes | Numeric citation position or a platform-specific composite position such as `web_search:1#0`. |
| `published_at` | string | Yes | Source publication date/time as supplied; not globally normalized. |
| `domain` | string | Yes | Lowercased source domain or host label. |
| `snippet` | string | Yes | Cited excerpt, summary, or retrieval snippet. |
| `prompt_id` | integer/null | Yes | Question-group identifier; not a row-level unique key. |
| `layer` | string | No | Top-level research dimension. |
| `subcat` | string | No | Subcategory within `layer`. |
| `record_hash` | string | No | SHA-256 of the normalized 12-field source record. |

## Key guidance

- Use `record_id` as the physical row identifier.
- Use `prompt_id` to group records belonging to the same benchmark question.
- Use `record_hash` to identify exact normalized duplicates.
- Preserve missing values instead of coercing them to zero or synthetic dates.
- Normalize `published_at` for analysis in a derived dataset rather than rewriting the canonical release.
