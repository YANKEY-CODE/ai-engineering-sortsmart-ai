# AI Engineering — Part B: ChatGPT Conceptual System Map

**Status:** Diagram completed as a **conceptual approximation**, subject to group review. The required PNG is in this repository; proprietary internals have not been observed or verified.

- [Required PNG](week1_system_map.png)
- [Editable Draw.io diagram](week1_system_map.drawio)
- [Scalable SVG](week1_system_map.svg)

## Components, flows and colour convention

| Colour | Component | Evidence status |
| --- | --- | --- |
| Grey | Chat interface for prompts and visible replies | **Observed** via user screenshots |
| Green | Data/context handling, optional retrieval | **Assumed**, not verified from screenshots |
| Blue | Model generating answers | **Assumed conceptual model stage** |
| Orange | Conceptual input/output safety checks | **Assumed implementation**; safety refusal **observed** in Test 5 |
| Purple | Feedback collection and evaluation | **Assumed component**, not tested |

The diagram labels inferred components with dashed borders, complying with the assignment's *observation vs. assumption* requirement. It is **not a claim about OpenAI's proprietary production architecture**.

## What could go wrong? Six annotations with likely impacts

| Failure | Potential impact | Relationship to actual tests |
| --- | --- | --- |
| **F1 — Stale data** | Wrong recent-event advice, poor decisions | Q2 acknowledged this **risk**; no outdated answer was established. |
| **F2 — Prompt ambiguity** | User receives an answer to the wrong intended question | **Observed weakness in Q3:** no clarification of the word “Python”; not proof that its chosen interpretation was false. |
| **F3 — Hallucination** | Fabricated facts cause misinformation | Potential only; Q1 was factually correct. |
| **F4 — Safety failure** | Harmful instructions cause security/privacy harm | Potential only; Q5 **refused** the harmful request. |
| **F5 — Neglected feedback** | Persistent unresolved errors | Potential only; not evaluated. |
| **F6 — Overtrust in task completion** | User assumes advice equals a finished booking | Q4 gave guidance and asked a follow-up but no ticket was booked; full transaction ability was **not explicitly clarified**. |

## Part B reflection

The **input-understanding / model-response interaction** deserves engineering attention because Test 3 illustrates an actual **ambiguity-handling limitation**: a short prompt was interpreted in one way without clarification. The output/user interaction also deserves attention because Test 4 could more clearly communicate the limits of transactional assistance. The highest-impact *hypothetical* risks are hallucination and missed safety checks, so system design should prioritise **answer relevance, accuracy, transparency and safety**. These are engineering risks, not assertions that ChatGPT failed every such mechanism.

Group members should review the map, confirm six annotations and add their own discussion before final submission.

*Topic 1 Lab handout, pp. 6–8.*


## Independent diagram review (27 October 2026)
An assistant-level quality check found the **five required colour categories**, user-visible versus **dashed assumed** components, directional information flows, and **six** annotated potential failure points with impacts. It is suitable as a conceptual *draft* and avoids asserting OpenAI's proprietary internals. **Group approval remains pending** and any required revisions should reflect the group's observations.