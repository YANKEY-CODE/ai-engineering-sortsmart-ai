# AI Engineering — Topic 3 Parts B/C: Pipeline Decisions and Evidence

**Project:** SortSmart AI · **Student:** Lai Yan Qi (A24AI0109) · **11 November 2026**  
**Version:** `week3-v1` · **Selected pathway:** A (PDF/TXT) · **Dataset:** course-supplied **synthetic practice**, not waste policy.

## Decision 1 — Match Topic 2 rather than executing all pathways

SortSmart's Topic 2 specifies a *text input* household waste assistant with authoritative document-grounded answers. Photo recognition is expressly out of scope. Therefore use **Pathway A (PDF/TXT)** only. Traceability: **FR2** (clickable source), **RAI1** (claim-source provenance), **RAI3** (source freshness / municipality), **NFR3** (maintainable source refresh). The future official sources named in `docs/week3_data_inventory.md` must be reviewed and permissions checked before replacing the practice corpus.

## Decision 2 — Observable comparison (B3)

Both methods processed the **same extracted text** with a **160-character target maximum**, an intentionally small setting for the short synthetic inputs. We did not alter source meanings, infer waste labels or perform embedding/training. The fixed method slices arbitrary character boundaries; the paragraph-aware method uses observed `Section N:` and `Q:` cues and blank lines, packing blocks within the limit (oversize blocks may still require fixed splitting).

| Source | Clean characters | Fixed 160-char chunks | Paragraph-aware 160-char chunks |
|---|---:|---:|---:|
| S01 | 425 | 3 | 5 |
| S02 | 170 | 2 | 2 |

**Chosen:** paragraph-aware, `CHUNK_SIZE=160` (PDF and TXT), because the PDF's first chunk ends after the demo header and subsequent chunks begin at meaningful sections; fixed slicing cuts across source-section text. In the TXT sample both methods happen to make 2 chunks, but the structure-aware method retains FAQ question boundaries more clearly. The PDF was read as **1 page**, and PDF chunks carry `page=1`; TXT chunks have `page=null` rather than a fabricated PDF page.

**Accepted trade-off:** the custom section/Q-A cues are simple, sample-specific heuristics and may not generalise to Malaysian government PDFs, multiple-column layouts, tables or OCR scans. A 160-character target is suitable for *these tiny teaching files*, not a vetted optimal setting for a later embedding/retrieval model. Verify with approved real documents and retrieval evaluation before adjusting the chunking configuration.

## Decision 3 — Part B outputs and stage contracts

| Stage | Contract / evidence | Failure response |
|---|---|---|
| **Ingest** | Explicit S01 PDF / S02 TXT present under `data/raw/`, readable, nonempty | Stop with `FileNotFoundError` for missing source; do not quietly use a different dataset |
| **Inspect** | `pypdf` extracts content; UTF-8 TXT loads; observed 425+170 clean characters | Stop / flag empty or unreadable extraction, unsupported suffix |
| **Prepare** | Whitespace normalization preserves newlines; section-aware chunks max 160 characters | Raise for invalid chunk size, invalid method, or missing records |
| **Validate** | Reload exported JSONL, check unique IDs, text length, source coverage and practice-only flags | Stop for empty or malformed output, duplicate IDs, missing metadata, wrong source set |
| **Store** | `data/processed/prepared_text.jsonl` exists, nonempty, with **7 records** | Stop for missing/zero-byte output; inspect actual content, not just file existence |
| **Record lineage** | S01 and S02 source hashes, output hash, record IDs and processing method in `data/week3_manifest.json` | Stop if any recorded source/output checksum or record count disagrees |

**Part B results:** **2 sources**, **7 prepared records**, output bytes **4759**, output SHA-256 `bf0ed47e57c0b8482b453ad64165c179ea27c8897bf32bce7e4700ded3aadeb9`. Actual source fingerprints are in `data/week3_manifest.json`. The prepared record count is a *processing measurement*, not a model performance score.

## Decision 4 — Pipeline orchestration, batch vs streaming, ETL vs ELT

**Batch:** Two small, curated documents change infrequently and can be prepared on demand. Streaming introduces complexity with no requirement for live data. The user-facing application is a later stage; this lab processes static sources offline.

**ETL chosen (extract → transform → load):** extract PDF/TXT into text; inspect and normalize; chunk + validate; then store a prepared JSONL with provenance. Raw files remain separate from processed outputs for auditable comparison. This is not a database ELT warehouse or model-training pipeline.

**Repeatability:** Part C re-runs the same transformation twice with identical sources/configuration, and compares source paths, SHA-256 hashes, sizes, output SHA-256, record count, source-to-record IDs, and Part B/Part C output identity. Result: **PASS**, 8/8 checks. Timestamps on the per-run manifest may change, by design; this proves only same-environment deterministic processing, not cross-machine reproducibility.

## Decision 5 — Source provenance, access and Responsible AI limitations

- `S01` and `S02` are **synthetic academic-domain examples** provided only for teaching. They are NOT official Malaysian environmental rules, and must not be cited as such.
- Raw source copyright/redistribution rights are **not independently verified**. Do not upload the original ZIP/PDF/TXT to the public GitHub repository without permission. The local submission package contains derived practice outputs for student review; confirm publishing rights before committing any full derived texts publicly.
- Real SortSmart data replacement: review permitted current material from JPSPN/DOE/KPKT, record exact URL/source owner, retrieval/publication date, jurisdiction, licensing, extraction loss, and human approval before downstream indexing; specifically check the 2006 JPSPN document for staleness and local applicability.
- This lab does not run an LLM, retrieval index, answer generation, ground-truth classification, citation-support audit, hazardous-item safety tests, or a web service. Topic 2 metrics (NFR/RAI) remain **proposed evaluation targets**, not measured achievements.
- No personal information, credentials or model API keys are required or used.

## Distinct manifest roles and paths

- `data/week3_manifest.json` — **Part B**, source→prepared output lineage + file hashes + record IDs.
- `data/processed/prepared_text.jsonl` — **Part B** clean, chunked, metadata-bearing text.
- `data/pipeline_v1/documents/prepared_text.jsonl` — **Part C** repeatable full execution output.
- `data/pipeline_v1/documents/pipeline_manifest.json` — **Part C** input/source fingerprints, stage contracts, output fingerprint, source-to-record mapping, run timestamp.
- `data/pipeline_v1/documents/repeatability_smoke_test.json` — **Part C** comparisons and PASS evidence.

**Design connection:** The diagram in `docs/week3_pipeline_diagram.png` expands only the **data / curated-source component** of `docs/week2_architecture_v1.png`; the full AI answer route remains planned for later weeks.
