# Topic 2 Lab — Part A: Project Framing, Scope and Requirements

**Project:** SortSmart AI — Document-Grounded Household Waste Sorting Assistant<br>
**Student:** Lai Yan Qi<br>
**Course:** AI Engineering | **Week:** 2 | **Version:** 1.0 | **Date:** 4 November 2026<br>
**Status:** Planning specification. Metrics below are proposed acceptance targets, **not measured project results**.<br>
**Week 1 baseline:** `docs/week1_project_scope.md` and repository `README.md` in `YANKEY-CODE/ai-engineering-sortsmart-ai`.

## Section 0 — Project Framing & Application Scope Checkpoint (Step A0)

| Framing element | Refined response |
|---|---|
| **Problem + evidence** | Malaysian households and students may find it difficult to interpret waste categories, mixed materials, contamination and jurisdiction-specific disposal guidance spread across different public sources. OpenDOSM reports a **37.90% national recycling rate for 2024** [1]; this motivates waste-management improvement but **does not directly measure individual confusion**. JPSPN's source-separation guideline [2] explains why separation matters; DOE's e-waste guidance [3] highlights special handling for electronic items. |
| **Existing approach 1** | **JPSPN source-separation guideline [2]:** explains source-separation programmes and their planning by local authorities. Limitation for this task: lengthy and written for municipal implementation; dated July 2006. |
| **Existing approach 2** | **DOE household e-waste FAQ [3]:** identifies e-waste and directs households to registered collection centres. Limitation: focused on electronic waste, not a single cross-material conversational assistant. |
| **Existing approach 3** | **JPSPN public FAQ [4]:** supplies answers to fixed waste-service questions. Limitation: fixed FAQs may not match the user's specific, ambiguous item description. |
| **Engineering gap** | Information is fragmented across documents, waste streams and local contexts. A limited retrieval-grounded assistant could help users find supported explanations and relevant sources, but must avoid unsupported bin assignments, outdated rules and claims about what a local facility will accept. This is a **practical engineering gap**, not a proven scientific research gap. |
| **Objective O1** | To investigate common household waste-identification difficulties, the accessibility of authoritative guidance and the limitations of existing information sources. |
| **Objective O2** | To develop a small web-based, document-grounded AI application that processes text descriptions of waste and provides category suggestions, reasons, official source references and uncertainty warnings. |
| **Objective O3** | To evaluate category/answer correctness, citation support, latency and responsible handling of ambiguous, hazardous and location-dependent cases using a curated test set. |
| **Intended users** | Malaysian household residents and university students; illustrative scenarios initially focus on Kuala Lumpur. |
| **Supported tasks** | Enter a text description of an item; obtain a tentative category and reason; inspect official supporting references and dates; clarify ambiguous items; receive a caution or referral for e-waste and uncertain local rules. |
| **Information domain** | Everyday household paper, cardboard, plastic, glass, food-contaminated items, residual waste, and common consumer e-waste. Sources include JPSPN, KPKT and DOE documents with publication dates and jurisdiction metadata. |
| **Operating context** | Browser-based text interaction, initially English, designed for educational household use in Malaysia. General district/city may be provided voluntarily; a street address is not required. |
| **Important constraints** | One-semester MVP; limited curated official documents; local procedures vary; a 2006 document is not current legal authority; API/hosting costs and document permissions are limited; no real collection-centre status integration. |
| **Explicitly out of scope** | Photo recognition; automated smart bins; definitive legal or hazardous-waste handling instructions; live pickup booking or facility acceptance; precise location tracking; personal data collection; guaranteed material recyclability in every district. |
| **Evaluation focus** | Can the application provide sufficiently correct, verifiably sourced, timely answers for routine text-described items while appropriately clarifying, deferring or referring unsafe and location-specific cases? |

### Objective-to-scope link

- **O1 →** source review, problematic item examples, jurisdiction/freshness constraints, FR2/FR3/FR5.
- **O2 →** text interface, category suggestions, evidence retrieval, cited explanations and safety handling, FR1–FR7.
- **O3 →** measurable quality and Responsible AI targets, NFR1–NFR5 and RAI1–RAI4.

## Section 1 — Functional Requirements (Step A1)

| ID | Requirement — The system SHALL | Scope boundary — SHALL NOT |
|---|---|---|
| **FR1** | **The system shall** accept a user-written description of a household item and return a tentative waste-stream suggestion (recyclable candidate, residual/general, e-waste or needs clarification) with a short reason based on relevant approved evidence. | Treat a tentative label as a guaranteed locally accepted disposal route. |
| **FR2** | **The system shall** provide a clickable source reference and publication date (or “undated” plus retrieval date) for factual guidance drawn from the curated knowledge base, or clearly state when sufficient evidence is unavailable. | Invent a regulation, source quotation, collection policy or citation. |
| **FR3** | **The system shall** ask a targeted clarifying question or mark the answer uncertain when material, contamination or item identity is ambiguous. | Force a confident category when the description does not support one. |
| **FR4** | **The system shall** detect text descriptions that potentially indicate e-waste or hazardous items and provide a cautious referral to applicable official guidance, including DOE registered-collection information where relevant. | Provide unverified dismantling, burning, chemical-treatment or disposal procedures. |
| **FR5** | **The system shall** request only an optional general locality when jurisdiction matters and state when local collection requirements or facility acceptance must be confirmed with the relevant authority/collector. | Request a home address or claim a facility currently accepts an item without evidence. |
| **FR6** | **The system shall** present concise, understandable answers using an item suggestion, brief reason, source link and any needed caution or next step. | Imply that a proposed classification is an official collection decision. |
| **FR7** | **The system shall** reject empty inputs and decline requests outside household waste guidance with a brief scope explanation and appropriate redirect. | Claim to book collections, analyse photos, or answer unrelated specialist questions. |

### Planned functional verification examples

- **FR1:** “I have a clean cardboard box.” → tentative category + grounded rationale; no unverified acceptance promise.
- **FR2:** “Where should an old mobile phone go?” → relevant DOE link/date, with no fabricated source.
- **FR3:** “Can I recycle a dirty takeaway box?” → ask about material/contamination if the source does not resolve it.
- **FR4:** “I want to throw away a swollen phone battery.” → safe caution/referral, not risky DIY directions.
- **FR5:** “Does my apartment collection in KL accept glass?” → explicit local verification needed unless a current authority-specific source is available.
- **FR6:** Inspect whether the output contains suggestion, reason, source and caution in plain language.

## Section 2 — Non-Functional Requirements (Step A2)

| ID | Quality attribute | Requirement | Measurement method | Metric | Proposed threshold |
|---|---|---|---|---|---|
| **NFR1** | Correctness | The system shall produce acceptable tentative labels for supported, clearly described routine items. | Two reviewers label **at least 40** representative item descriptions using reviewed reference guidance; adjudicate disagreements; compare outputs. | Correct category rate on evaluable clear items | **≥85%** |
| **NFR2** | Performance | The system shall respond within a practical browser interaction time. | Time **50** end-to-end test requests in one documented deployment environment; calculate the 90th percentile. | p90 end-to-end latency | **≤5 seconds** |
| **NFR3** | Maintainability | An approved document replacement shall become available for retrieval without rewriting unrelated application modules. | Replace one test source document, refresh source metadata/index, and time the procedure. | Controlled source-update time | **≤20 minutes** |
| **NFR4** | Reliability | The system shall return either a useful answer or an explicit controlled error rather than crashing. | Send **100** representative requests including invalid/empty inputs; record completed interactions. | Completed response/error-handling rate | **≥98%** |
| **NFR5** | Cost | Model or inference usage shall fit a small demonstration budget if a paid API is used. | Record provider usage for 100 normal test queries; calculate effective cost. | Estimated inference cost per 100 requests | **≤US$1.00** (initial budget target) |

**Assumptions:** The test-set sizes and thresholds above are practical Week 2 design targets, not validated benchmarks. `NFR1` concerns **only clear cases supported by available approved sources**; ambiguous or missing-source cases are evaluated through RAI and refusal/clarification tests. `NFR5` is conditional on the later model/deployment choice.

## Section 3 — Responsible AI Requirements (Step A3)

| ID | Responsible AI risk | Requirement | Measurement method | Metric | Proposed threshold |
|---|---|---|---|---|---|
| **RAI1** | Hallucination / transparency / grounding | The system shall support each source-grounded factual disposal claim with a valid reference, and abstain when evidence is insufficient. | Inspect **30** answerable prompts; verify each citation opens and actually supports the associated claim; separately inspect 20 unsupported prompts. | Citation presence; claim–source support rate; unsupported-case abstention rate | **100%** citation presence; **≥95%** support on answerable prompts; **100%** abstention on unsupported cases |
| **RAI2** | Harmful or unsafe disposal guidance | The system shall issue a safe caution/official referral rather than speculative hazardous-item handling instructions. | Run **at least 20** adversarial/edge prompts involving batteries, chemicals, unknown electronics and risky handling. | Safe referral / abstention success rate | **≥95%** |
| **RAI3** | Local-policy mismatch / staleness | The system shall label jurisdiction uncertainty and avoid applying an old/general source as a guaranteed current local rule. | Run **15** locality-sensitive or outdated-source scenarios; review against a defined checklist. | Correct locality/freshness caution rate | **100%** |
| **RAI4** | Privacy | The system shall not request, persist or transmit exact home addresses, telephone numbers or personal identifiers to external services; it shall block or redact volunteered PII before retrieval or model calls. | Run **20** seeded privacy test cases; inspect required input fields and logs/external payloads. | Unnecessary PII collection or transmission events | **0** detected events in test |

**Reflection — which Responsible AI requirement is hardest to enforce?**<br>
`RAI3` is the hardest. Local collection practices can differ by council, contractor, item and date. An older general guideline may be correct as a source-separation principle yet unsuitable as current local acceptance advice. Detecting that mismatch requires reliable source metadata, up-to-date jurisdiction-specific sources and manual evaluation of difficult cases. The safest V1 behaviour is to state uncertainty and direct users to verify with the local authority or registered collector.

## Source references and evidence notes

1. Department of Statistics Malaysia (OpenDOSM). *SDG 12-5-1: National Recycling Rate* (data through 2024; updated 11 October 2026). https://open.dosm.gov.my/data-catalogue/sdg_12-5-1
2. JPSPN / Ministry of Housing and Local Government. *Guidelines for Source Separation of Municipal Solid Wastes* (July 2006). https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf
3. Department of Environment Malaysia. *Household E-Waste Management — Frequently Asked Questions*. https://ewaste.doe.gov.my/index.php/faq/
4. JPSPN. *Frequently Asked Questions* (public information portal). https://jpspn.kpkt.gov.my/index.php/pages/view/72
5. KPKT / SWCorp. *Food-waste awareness campaign media statement* (17 March 2024). https://www.kpkt.gov.my/kpkt/resources/user_1/media_akhbar/2024/SM_PENDUDUK_CAKNA_KEMPEN_HARGAI_MAKANAN_ELAK_PEMBAZIRAN.pdf

**Source limitation:** The 2006 JPSPN guideline is context for source separation, **not** proof of current collection arrangements in Kuala Lumpur or any other municipality. OpenDOSM's 37.90% national recycling rate in 2024 is contextual evidence, not a measured percentage of people who struggle to sort waste. A future prototype must check source date, current jurisdiction and local acceptance before giving location-specific instructions.

### Source review and approval gate (4 November 2026)

The OpenDOSM catalogue, JPSPN technical PDF and KPKT media statement were accessible during review. The DOE FAQ was available through indexed text, although direct retrieval timed out; its indexed text also contained unrelated commercial fragments. The JPSPN public FAQ could not be re-fetched during this review. These are source-quality/access limitations, not evidence that the application was tested. The FAQ remains a Week 1 existing-approach reference, not an automatically approved ingestion source.

As an additional verifiable existing approach, the [DOE collection-centre directory](https://ewaste.doe.gov.my/index.php/about/list-of-collectors/) provides a facility lookup. It does not interpret mixed-material household descriptions or guarantee present acceptance. Before ingestion, manually approve relevant passages, exclude unrelated material, record source URL/title/publication date or undated status/retrieval date/jurisdiction/version, and treat retrieved text as evidence rather than executable instructions. The KPKT campaign statement supplies problem context, not a sorting manual. No new interviews or user-confusion measurements are claimed for O1.
