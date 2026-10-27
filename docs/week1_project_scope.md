# Week 1 Project Scope — SortSmart AI

**Assignment:** AI Engineering, Topic 1 Lab, Part C (individual)  
**Project name:** SortSmart AI — Document-Grounded Household Waste Sorting Assistant  
**Domain:** Environmental sustainability / household waste management / AI information retrieval  
**Status:** Preliminary scope; refine in Topic 2.

## Problem Statement
Users may struggle to interpret whether everyday items are recyclable, residual waste or e-waste, particularly where the item is contaminated, made of mixed materials or subject to different local collection conditions. Government guidance is distributed across documents and webpages, and some source-separation guidance is written for municipal officers rather than household questions. SortSmart AI proposes a small AI-powered website to interpret **text descriptions** of items and return short, source-grounded explanations, uncertainty warnings and links to official sources. It will **not** guarantee that a particular facility accepts an item.

## Evidence of the Problem (two credible references)
**Evidence 1 (national context):** OpenDOSM reports Malaysia's 2024 national recycling rate as 37.90%. This supports the importance of waste-management improvement but does not by itself demonstrate individual user confusion.  
**Source:** Department of Statistics Malaysia, *SDG 12-5-1: National Recycling Rate*, data through 2024: https://open.dosm.gov.my/data-catalogue/sdg_12-5-1

**Evidence 2 (need for source separation):** JPSPN's municipal solid waste source-separation guideline explains that separating waste at source can improve recovery of recyclables and reduce disposal, and that actual plans must consider local conditions. The guideline was issued in 2006, so rules must be checked against newer and local guidance.  
**Source:** JPSPN, *Guidelines for Source Separation of Municipal Solid Wastes* (July 2006): https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf

**Additional safety evidence:** DOE explains that electronic waste can contain hazardous substances and should go to registered collection centres.  
**Source:** DOE, E-Waste FAQ: https://ewaste.doe.gov.my/index.php/faq/

## Initial Related Work / Existing Approaches (at least three)
1. **JPSPN source-separation technical guidelines**  
   Source: https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf  
   Key limitation: Written mainly for local authorities; long and not a conversational lookup experience for household users; dated 2006.
2. **Department of Environment household e-waste FAQ**  
   Source: https://ewaste.doe.gov.my/index.php/faq/  
   Key limitation: Authoritative for e-waste but not a unified helper for plastics, paper, glass, food waste and e-waste together.
3. **JPSPN general FAQ about waste-management services**  
   Source: https://jpspn.kpkt.gov.my/index.php/pages/view/72  
   Key limitation: A static FAQ may not address descriptions such as mixed-material packaging, dirty containers or uncertain local rules.

These are **existing solutions/resources**, not peer-reviewed comparisons. Topic 2 may add research studies.

## Engineering Gap / Limitation
Public information is fragmented and varies by waste stream, document age and jurisdiction. The gap to investigate is whether a **retrieval-augmented natural-language interface** can provide relevant, citation-grounded disposal guidance across documents while refusing to guess about hazardous or locally uncertain cases.

## Initial Project Objectives
- **O1:** To investigate challenges in household waste identification, source accessibility and the limits of existing waste guidance.
- **O2:** To develop a document-grounded AI web application that processes users' text descriptions and delivers supported waste sorting explanations with citations.
- **O3:** To evaluate classification/answer correctness, citation support, response latency and safety/uncertainty handling.

## Target Users
Household residents and university students in Malaysia, initially piloted with Kuala Lumpur examples. Users must verify municipality-specific collection rules.

## Data Sources (at least two public documents)
1. **JPSPN, Guidelines for Source Separation of Municipal Solid Wastes (PDF, 2006)** — https://jpspn.kpkt.gov.my/jpspn/resources/Images%20JPSPN/Sumber%20Rujukan/Garis%20Panduan%20Teknikal/Guidelines_for_Source_Separation_of_Municipal_Solid_Wastes.pdf
2. **KPKT, Media statement on a food-waste awareness campaign (PDF, 2024)** — https://www.kpkt.gov.my/kpkt/resources/user_1/media_akhbar/2024/SM_PENDUDUK_CAKNA_KEMPEN_HARGAI_MAKANAN_ELAK_PEMBAZIRAN.pdf
3. **DOE, E-waste FAQ (official web document)** — https://ewaste.doe.gov.my/index.php/faq/

The sources are linked rather than copied; check use and redistribution permissions. Before development, verify currency, applicability, and completeness for target items.

## Similar to EduAdvisor
Both propose a document-grounded AI assistant with source retrieval, a conversational interface, guardrails, a feedback mechanism and measurable answer quality.

## Different from EduAdvisor
SortSmart AI addresses waste classification and disposal guidance rather than academic policies. Its answers must handle material ambiguity, safety risks (e.g. batteries), varied collection rules and the age of official guidance.

## Responsible AI Risks (at least two)
1. **Incorrect/hallucinated guidance:** May make users dispose of items wrongly. Mitigation: require supporting sources; say when evidence is missing; human-verified test cases.
2. **Safety / hazardous items:** Wrong battery or e-waste advice may endanger people/environment. Mitigation: direct to DOE/authorised collectors, avoid unverified handling procedures.
3. **Locality and stale information:** A rule valid in one region or year may be misapplied. Mitigation: specify jurisdiction, label document dates, and defer on uncertain local rules.
4. **Privacy:** Users might share unnecessary location details. Mitigation: request only general locality, avoid storing personal addresses.

## Proposed One-Semester MVP
**In scope:** text-input web page, limited document ingestion, retrieval/search, cited responses, category suggestion, safety/uncertainty notices and curated evaluation.  
**Out of scope:** image-recognition training, automated bin control, definitive legal compliance, live collection-centre availability and nationwide real-time pickup scheduling.

**Initial evaluation metrics:** label accuracy on annotated text-item queries; citation relevance/faithfulness; percentage of ambiguous or hazardous prompts safely escalated; latency in seconds.
