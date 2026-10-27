# Week 1 Conceptual System Map — Part B (GROUP TASK)

**Status:** NOT COMPLETED. The group must map the **assigned existing AI system from Part A**, not SortSmart AI. The required PNG should be named `docs/week1_system_map.png`.

## Draw.io steps
1. Open https://app.diagrams.net/ → Blank Diagram → Landscape.
2. Title: `[Assigned AI System] — Conceptual AI System Map`.
3. Create the relevant high-level nodes. Green = data/pipeline; blue = model/AI; orange = guardrails/safety; purple = evaluation/monitoring; grey = interface.
4. Connect nodes with labelled arrows explaining flow; distinguish **observed behaviours** from **engineering assumptions**.
5. Use dashed borders or `Assumed Component` for unverified/proprietary internals.
6. Write **at least five plausible failure points**, each with a likely impact, in red.
7. Export **PNG** as `docs/week1_system_map.png` and keep the editable `.drawio` if possible.

## Potential failure scenarios to adapt, NOT claims of observed incidents
- Old or missing data → outdated response / recommendations.
- Inappropriate preprocessing → poor input understanding.
- Model error or hallucination → misleading answer.
- Safety/filter failure → harmful content shown.
- Biased ranking or uneven performance → unfair user experience.
- Feedback not acted on → recurring mistakes.

## Part B reflection
Which component has the most potential failure points, and where should engineering effort focus? Connect to at least one measured quality dimension. [COMPLETE FOR YOUR ACTUAL GROUP MAP]
