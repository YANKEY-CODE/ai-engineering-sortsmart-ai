# SortSmart AI — Document-Grounded Waste Sorting Assistant

> A proposed AI Engineering semester project helping Malaysian households and students understand how to separate household waste and handle common e-waste, using cited public Malaysian guidance.

**Status:** Week 1 project framing / planning. This repository is an engineering record, **not yet a functioning AI application**.

## Problem Statement
People who want to dispose of everyday waste correctly must interpret material categories, contamination conditions, and local collection requirements across several sources. Wrong assumptions may contaminate recyclable collections or lead to unsafe e-waste disposal. SortSmart AI proposes a document-grounded question-answering assistant that explains classifications in plain language and links to official sources.

## Evidence of the Problem
- The Department of Statistics Malaysia reports a **37.90% national recycling rate in 2024**; this is a national indicator, **not evidence that any particular individual is confused**: https://open.dosm.gov.my/data-catalogue/sdg_12-5-1
- JPSPN's *Guidelines for Source Separation of Municipal Solid Wastes* describes the need for source separation and local implementation considerations (2006): https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf
- The Department of Environment advises that household e-waste go to registered collection centres: https://ewaste.doe.gov.my/index.php/faq/

## Initial Related Work / Existing Approaches
1. **JPSPN source-separation guidelines** — authoritative guidance, but written primarily for local authorities rather than conversational household questions. https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf
2. **Department of Environment e-waste FAQ / collection-centre guidance** — authoritative and practical for e-waste, but limited to that waste stream. https://ewaste.doe.gov.my/index.php/faq/
3. **JPSPN public FAQ on waste collection** — useful for fixed policy questions, but not tailored to detailed, ambiguous item descriptions. https://jpspn.kpkt.gov.my/index.php/pages/view/72

## Engineering Gap / Limitation
Information is distributed across static resources that cover different waste categories and audiences. The proposed system will test whether retrieval-grounded answers can make relevant guidance easier to find **without inventing rules**, especially when local requirements or a user's item description are ambiguous.

## Project Objectives
- **O1:** Investigate problems users face in identifying waste categories and finding trustworthy, locally applicable disposal guidance.
- **O2:** Develop a small web-based, document-grounded AI assistant that classifies text descriptions of household waste, retrieves source passages and provides cited guidance.
- **O3:** Evaluate answer correctness, retrieval/citation groundedness, response latency and safe handling of uncertain or hazardous items.

## Target Users
Malaysian households and university students; initial demonstration examples can focus on Kuala Lumpur, with a clear notice that local collection instructions must be checked against the relevant authority.

## Data Sources
1. JPSPN — *Guidelines for Source Separation of Municipal Solid Wastes* (PDF; July 2006): https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf
2. KPKT — *KPKT media statement on the food-waste awareness campaign* (PDF; 2024): https://www.kpkt.gov.my/kpkt/resources/user_1/media_akhbar/2024/SM_PENDUDUK_CAKNA_KEMPEN_HARGAI_MAKANAN_ELAK_PEMBAZIRAN.pdf
3. DOE — *E-Waste Management Frequently Asked Questions* (web document): https://ewaste.doe.gov.my/index.php/faq/

Note: The JPSPN guidelines are from **2006** and must not be treated as a definitive statement of current local collection rules. Only link to source files; do not redistribute potentially copyrighted PDFs in this public repository without permission.

## Responsible AI Risks
- **Hallucination / wrong category:** an unsupported claim may lead to contamination or incorrect disposal.
- **Hazardous waste:** incorrect advice for batteries, chemicals or electronics can cause harm; refer users to official guidance, and avoid speculative handling instructions.
- **Local-policy mismatch / outdated documents:** advice may not apply in every Malaysian state or district; ask for location and flag uncertainty.
- **Privacy:** do not collect precise addresses or personal information unless necessary.

## Proposed Evaluation
Prepare a small test set of item descriptions with ground-truth labels and relevant official citations. Score category accuracy, factual and citation support, safe deferral rate for ambiguous/hazardous examples, and response latency. The test set and scores will be added in later weeks.

## Weekly Progress
| Week | Focus | Deliverable | Status |
| --- | --- | --- | --- |
| W1 | Existing AI analysis, system map, individual scope | Observation sheet, map, scope, README | In progress — group testing needed |
| W2 | Requirements and evaluation criteria | Refined specifications | Planned |
| W3+ | Implementation in Colab and website | Prototype and tests | Planned |

## Repository Structure
- `docs/week1_project_scope.md` — individual Part C scope
- `docs/week1_observation_sheet.md` — **group Part A draft; must be completed with actual observations**
- `docs/week1_system_map_template.md` — **group Part B instructions; export the real diagram as `docs/week1_system_map.png`**
- `docs/week1_reflections.md` — prompts for reflection, to complete after group sharing
- `data/`, `src/`, `notebooks/`, `evaluation/`, `prompts/` — later engineering evidence

## Week 1 Submission Status
**Not ready to submit:** Part A and Part B depend on your assigned group system and actual observed evidence. The required `docs/week1_system_map.png` is now included. Final checks are in `SUBMISSION_CHECKLIST.md`.


## Week 1 group evidence update — ChatGPT
Part A is for **ChatGPT** (Groups 1–2). An **in-session five-prompt response sample** is recorded in [the observation sheet](docs/week1_observation_sheet.md); this is not an independently repeated test and screenshot evidence still needs to be collected. Part B has an [editable Draw.io map](docs/week1_system_map.drawio), a [viewable SVG](docs/week1_system_map.svg), and [failure-point notes](docs/week1_system_map_notes.md). The [required PNG system map](docs/week1_system_map.png) is uploaded. Group review and evidence screenshots are still needed. Read [the updated checklist](SUBMISSION_CHECKLIST.md) for all outstanding items.