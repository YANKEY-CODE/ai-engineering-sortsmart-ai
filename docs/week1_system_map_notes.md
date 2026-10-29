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

## Failure-point-to-component mapping (clarifies the diagram)

| Failure label | Relevant stage or interaction | Quality dimension |
| --- | --- | --- |
| F1 — Stale data | **Data/context** supplying old or incomplete information to the model | Accuracy / reliability |
| F2 — Prompt ambiguity | **User input → input processing → model**; Q3 illustrates a real interpretation weakness | Answer relevance / transparency |
| F3 — Hallucination | **Model generation → output checking**; unsupported claims might pass into the response | Accuracy / reliability |
| F4 — Safety failure | **Output guardrails → user-visible answer**; harmful content could be shown | Safety / security |
| F5 — Missed feedback | **Feedback collection → evaluation**; errors could persist | Monitoring / reliability |
| F6 — Overtrust in task completion | **Output response → user**; booking guidance might be mistaken for an actual booking | Transparency / scope handling |

The six red boxes in the diagram are grouped as a failure-point register. The mapping above identifies the stage for each box; the red boxes do **not** represent six incidents established by testing. The **model/output-response pathway** has three related risks (F3, F4 and F6), so it is reasonable to concentrate additional checks there, while also addressing the **observed Q3 ambiguity weakness** at the input/model interaction.

## Part B reflection

The **model-to-output-checking and user-response pathway** has the largest cluster of related annotations in the conceptual map: F3 (hallucination), F4 (missed safety problem) and F6 (overtrust in task completion). This suggests concentrating engineering effort on **answer accuracy and reliability**, **safety**, and **transparency about completed actions**. Separately, Test 3 showed an **observed ambiguity-handling weakness** at the input/model interaction: ChatGPT interpreted “Is Python good?” as a programming-language question without asking for clarification. Test 4 also lacked an explicit statement about direct ticket-purchasing capability. The other failure points remain plausible risks rather than confirmed incidents.

Group members should review the map, confirm six annotations and add their own discussion before final submission.

*Topic 1 Lab handout, pp. 6–8.*


## Independent diagram review (27 October 2026)
An assistant-level quality check found the **five required colour categories**, user-visible versus **dashed assumed** components, directional information flows, and **six** annotated potential failure points with impacts. It is suitable as a conceptual *draft* and avoids asserting OpenAI's proprietary internals. **Group approval remains pending** and any required revisions should reflect the group's observations.