# AI Engineering — Part B: ChatGPT Conceptual System Map

**Status:** Conceptual group map prepared; discuss with your group and export the **required PNG** from the editable Draw.io source. Internal architecture is not verified.

- **Viewable image:** [week1_system_map.svg](week1_system_map.svg)
- **Editable source:** [week1_system_map.drawio](week1_system_map.drawio)
- **Lecturer-required PNG:** [week1_system_map.png](week1_system_map.png) — now uploaded.

## Colours and principal stages
- **Grey — User interface:** prompt entered and natural-language reply. **Observed** in this ChatGPT conversation.
- **Green — Context/data and optional retrieval:** possible information processing / tools. **Assumed, conditional**.
- **Blue — Model:** candidate reply generation. **Assumed internal component**, not proprietary architecture.
- **Orange — Input and output guardrails:** conceptual checking/routing. **Assumed**, though a refusal was observed in Q5.
- **Purple — Feedback and evaluation:** possible ratings/reports and monitoring. **Assumed**.

Arrows represent a high-level engineering approximation: prompt → possible guardrails → model → output checks → chat response; context and optional retrieval may assist model generation; feedback may inform monitoring. No exact deployment topology is asserted.

## B3 — What could go wrong? (at least FIVE failures and impacts)
| ID | Failure scenario | User/system impact | Observed? |
| --- | --- | --- | --- |
| F1 | Stale/missing information | Misleading recent-event answers | Potential only |
| F2 | Input ambiguity misunderstood | Wrong intent, irrelevant answer | Potential; Q3 recognised ambiguity |
| F3 | Hallucinated statement | Misinformation and poor decisions | Potential; not observed in Q1 |
| F4 | Unsafe generated response escapes safeguards | Privacy/security harm to account owners | Potential; Q5 actually refused |
| F5 | Feedback not reviewed | Recurrent unresolved errors | Potential; not tested |
| F6 | User mistakes guidance for a completed action | Missed flights or unnecessary cost | Potential; Q4 disclosed limitation |

## Part B reflection
The model/output-safety interaction has the most consequential related failure modes (F3, F4 and F6): unsupported model assertions or weak output safeguards could misinform users or lead to misuse. Engineering effort should prioritise **accuracy**, **safety**, **transparent uncertainty** and **clear action-state reporting**. These are hypothetical failure points; the short Part A test did not establish actual failures in these stages.

*Reference: Topic 1 Lab, pp. 6–8. Inferred components are marked dashed, per the lab instructions.*