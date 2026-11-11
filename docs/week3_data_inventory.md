# AI Engineering — Topic 3 Part A: Data Inventory

**Project:** SortSmart AI — Document-Grounded Household Waste Sorting Assistant  
**Student:** Lai Yan Qi (A24AI0109) | **Lab date:** 11 November 2026 | **Version:** week3-v1  
**Evidence:** `notebooks/week3_pipeline.ipynb` (executed), `data/week3_manifest.json`

## A1 — Requirements-to-data traceability

| Week 2 requirement | Data needed | Why this pathway / limitation |
|---|---|---|
| **FR2 — Cited source references** | Traceable PDF/TXT passages, source identity, and page ID where applicable | Document parsing and source metadata are prerequisite engineering stages, but no citations for real disposal rules are possible with this practice corpus. |
| **RAI1 — Verifiable grounding** | Consistent source ID + checksum for every prepared chunk | Lineage makes future claim-to-source audits feasible. It does **not** prove a claim is actually supported. |
| **RAI3 — Jurisdiction and document currency** | Publication/version and jurisdiction metadata | Test the metadata schema; these synthetic sources have no waste-guidance jurisdiction or official publication date. |
| **NFR3 — Controlled document refresh** | Deterministic transforms, stable record IDs, rerunnable pipeline | Repeated same-input processing produces identical output bytes. This is *not* the planned timed document replacement evaluation. |

Topic 2 architecture used: **curated source library → official evidence retrieval**, including a versioned update path. Topic 3 implements *only the upstream document-ingestion data branch*, not the AI/retrieval application. Topic 2 explicitly excludes images/photo recognition.

## A2–A4 — Dataset selection and ingestion evidence

**Actual intended SortSmart sources for later approved ingestion (not used in this Week 3 run):**

- JPSPN, *Guidelines for Source Separation of Municipal Solid Wastes* (July 2006): https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf — outdated for current local collection policy; require manual review.
- Department of Environment, household e-waste FAQ: https://ewaste.doe.gov.my/index.php/faq/ — live webpage needs an approved capture/conversion loader; confirm currency and avoid unrelated page content.
- KPKT food-waste awareness media statement (March 2024): https://www.kpkt.gov.my/kpkt/resources/user_1/media_akhbar/2024/SM_PENDUDUK_CAKNA_KEMPEN_HARGAI_MAKANAN_ELAK_PEMBAZIRAN.pdf — campaign context, *not* a complete sorting rulebook.

The user-provided `Topic_3_Dummy_Datasets.zip` was used **only because no approved, redistributable domain documents were provided for this lab session**. The supplied pack states that all samples are synthetic educational examples. Public redistribution permission for the pack itself has not been established, so **the raw ZIP/PDF/TXT should not be committed to the public repository without permission**.

| Source ID | Filename / raw path | Type and purpose | Version / owner | Access / rights | Observed ingestion evidence |
|---|---|---|---|---|---|
| **S01** | `topic3_dummy_datasets/01_documents/student_handbook_demo.pdf` | PDF, text extraction / section-aware chunking practice | "2026 Demo Edition" in PDF; Teaching Team | Supplied practice pack, public redistribution not verified | 1 readable page, **425** cleaned characters, source SHA-256 begins `3dc6270e4a2d…`; shows registration, attendance, graduation and academic support sections |
| **S02** | `topic3_dummy_datasets/01_documents/faq_demo.txt` | UTF-8 TXT, question-answer chunking practice | Undated; synthetic course-pack example | Supplied practice pack, public redistribution not verified | 1 readable TXT record, **170** cleaned characters, source SHA-256 begins `05461ed704d8…`; two FAQ questions and responses |

**Separate inspection examples:** the PDF starts with `SAMPLE STUDENT HANDBOOK - SYNTHETIC DATA` and has a `Section 1: Registration` heading; the TXT starts `DEMO FAQ - synthetic content` and contains the question `Where do I find course information?`. Those are genuine parsed samples shown by the notebook, not inferred from filenames.

**Observed limitations:** The PDF is digital text (readable with `pypdf`), not a scanned document. These synthetic examples contain no waste-category labels, permitted disposal rules, Malaysian jurisdiction, official policy publication metadata, or license grant for public redistribution. The future production loader must review real source rights, table extraction, publication/retrieval date, scope/jurisdiction and source version.

## Raw vs prepared storage

- **Input (local Colab/runtime only):** `data/raw/topic3_dummy_datasets/01_documents/{student_handbook_demo.pdf,faq_demo.txt}`. The raw ZIP is **not** a GitHub submission artefact.
- **Part B:** `data/processed/prepared_text.jsonl`, `data/processed/chunking_comparison.json`, `data/week3_manifest.json`.
- **Part C:** `data/pipeline_v1/documents/prepared_text.jsonl`, `pipeline_manifest.json`, `repeatability_smoke_test.json`.
- `week3_manifest.json` records Part B source-to-output links; `pipeline_manifest.json` records the executed Part C run. Timestamps on manifests may differ between runs. Record texts are stable for the same inputs and processing configuration.

**Data safety:** All prepared examples are marked `SYNTHETIC_PRACTICE_ONLY` and `approved_for_end_user_guidance=false`. Never use them to populate a user-facing waste-sorting knowledge base or claim source-grounded disposal accuracy.
