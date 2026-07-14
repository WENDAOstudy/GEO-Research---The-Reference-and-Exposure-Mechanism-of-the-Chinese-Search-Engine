# Dataset card

## Dataset summary

CN-GEO Citation Dataset is a structured corpus of citation and retrieval-result records linked to benchmark prompts across Chinese generative search platforms. The unit of observation is one source result returned for a prompt on a platform.

## Intended uses

- Citation-source and domain-distribution analysis
- Source-exposure comparison across platform codes
- Prompt-category and time-sensitivity research
- Retrieval diversity, duplication, and missingness analysis
- Reproducible GEO benchmark studies

## Out-of-scope uses

- Treating snippets as complete or authoritative source documents
- Inferring user identity or personal attributes
- Using `prompt_id` as a row-level primary key
- Interpreting platform codes without an externally verified codebook

## Dataset composition

- 214,119 records
- 609 non-null `prompt_id` values
- 12 platform codes
- 7 top-level dimensions
- 32 dimension/subcategory pairs
- 64 JSONL shards

## Processing

1. Records were separated using the source format's two-blank-line boundary.
2. Literal control characters inside JSON strings were escaped without dropping content.
3. Line endings were normalized to `LF`; surrounding whitespace was trimmed.
4. `domain` values were lowercased.
5. Integer-like `prompt_id` and `quote_index` values were typed as integers; platform-specific composite `quote_index` values were preserved as strings.
6. A stable source-order `record_id` and content-based SHA-256 `record_hash` were added.
7. Records were grouped by `layer` and `subcat`, then split into shards of at most 5,000 records.

No records were removed. Exact duplicates remain in the release and are quantified in the quality report.

## Provenance

The canonical source file was `aidso-results-v2-updated.txt`, a UTF-8 block-delimited text file. Its SHA-256 checksum, byte size, and record count are stored in `data/manifest.json`.

The source package did not provide a complete collection protocol, platform-code mapping, sampling frame, or comprehensive temporal coverage statement. Users should avoid inferring these details.

## Maintenance

Versioned changes should be documented in `CHANGELOG.md`. Schema-breaking changes require a new major version.
