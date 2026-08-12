# Skills Index

All skills in the BAO AI-Native BA Framework.

Install each skill via Claude.ai → Settings → Skills → Add Skill.

Invoke in any Claude Project chat with `/skill-name`.

---

| Skill | Status | Phase | Description | Trigger |
| --- | --- | --- | --- | --- |
| `/project-charter` | ✅ ready | 1 · Project Setup | Structures kickoff notes / S&V / WBS into the project charter. Output: `01_project_context.md`. | Start of a new project |
| `/tech-context` | ✅ ready | 1 · Project Setup | Captures stack, integrations, architecture, constraints, glossary. Output: `03_tech_context.md`. | Need technical grounding for BA work |
| `/pc-from-zero` | ✅ ready | 1 · Project Setup | Builds the Product Context (product source of truth) from scratch, source by source. Output: `product_context.md`. | No Product Context yet — build it |
| `/stakeholder-analysis` | ✅ ready | 1 · Project Setup | Maps internal / client stakeholders, decision authority, RACI. Output: `02_stakeholders.md`. | Need a stakeholder map for a project |
| `/ba-communication-plan` | ✅ ready | 1 · Project Setup | Meeting cadence, contact matrix, escalation path. Output: `comm_plan.md`. | Need to define communication structure |
| `/ba-governance` | ✅ ready | 1 · Project Setup | Prioritization, approvals, change control, DoR / DoD. Output: `governance.md`. | Need to define governance approach |
| `/rma-generation` | ✅ ready | 1 · Project Setup | Requirements lifecycle, traceability, attributes, tooling. Output: RMA document. | Formalize requirements management |
| `/ba-approach-and-activities` | ✅ ready | 1 · Project Setup | BA role, activities, deliverables, mutual commitments + kickoff agenda. | Kickoff / BA role alignment |
| `/elicitation-prep` | ✅ ready | 2 · Discovery & Elicitation | Structured question list for a session (project-wide / epic / sprint). Output: `questions_list_<scope>.md`. | Preparing for a client session |
| `/open-questions-per-epic` | ✅ ready | 2 · Discovery & Elicitation | Per-epic open-questions register, routed and prioritized. Output: `open_questions_per_epic.xlsx`. | Open questions before refining an epic |
| `/analyze-incoming` | ✅ ready | 2 · Discovery & Elicitation | Explains an incoming item and routes it to the next action. Output: triaged item list. | Client / dev input to process |
| `/pc-update` | ✅ ready | 2 · Discovery & Elicitation | OLD→NEW find/replace edits bringing the Product Context to current state. | Commit decided changes to the PC |
| `/call-summary` | ✅ ready | 2 · Discovery & Elicitation | Client-facing summary of a session from its transcript. Output: `call_summary_<date>.md`. | After a client call |
| `/decompose-wbs-epic` | ✅ ready | 3 · Requirements & Modelling | Splits a WBS epic into vertical INVEST stories grouped under WBS parents. Output: story list + split pattern + gaps. | Break a WBS epic into stories |
| `/story-map-per-epic` | ✅ ready | 3 · Requirements & Modelling | Builds a story map from the approved decomposition. Output: `story_map_<epic>.xlsx` (Miro-importable). | Story map for an epic |
| `/ears-ac` | ✅ ready | 3 · Requirements & Modelling | Writes Acceptance Criteria in EARS house style for an approved story. | AC for an approved story |
| `/ac-validation` | ✅ ready | 3 · Requirements & Modelling | Reviews AC for coverage and quality, no rewrite. Output: coverage report. | Check AC before refinement |
| `/requirements-gap-check` | ✅ ready | 3 · Requirements & Modelling | Cross-project scan for gaps, inconsistencies, duplicates, orphans. Output: health report. | Before refinement / milestone |
| `/flow-build` | ✅ ready | 3 · Requirements & Modelling | Builds editable stakeholder-review flowcharts for an epic. Output: FigJam file (one section per flow). | Flows for client review |
| `/design-validation` | ✅ ready | 3 · Requirements & Modelling | Validates a design / flow PDF against the PC, findings only. Output: findings report. | Review a design vs requirements |
| `/epic-pc-consistency` | ✅ ready | 3 · Requirements & Modelling | Validates a decomposed epic against the PC and neighbouring epics. Output: categorized findings. | Check an epic vs the PC |
| `/nfr-quality` | ✅ ready | 3 · Requirements & Modelling | Generates or validates NFRs (ISO 25010 + Utility Tree). | Define or review NFRs |
| `/jira-split` | ✅ ready | 4 · Tickets & Traceability | Maps and splits a WBS epic into the Jira ticket structure + subtasks. | Split an epic into Jira tickets |
| `/jira-fill` | ✅ ready | 4 · Tickets & Traceability | Writes finalized story + AC into the matching Jira tickets. | Fill AC into Jira tickets |
| `/traceability-matrix` | ✅ ready | 4 · Tickets & Traceability | Builds an epic → story → subtask coverage + progress matrix from Jira. Output: `traceability-matrix.xlsx`. | Need full project coverage overview |
| `/changelog` | ✅ ready | 5 · Iterative | Writes one ready-to-paste Change Log row from a decided change. | Log a baselined change |

---

## Status Legend

| Status | Meaning |
| --- | --- |
| ✅ ready | Skill is complete and tested — install and use |
| 🚧 in progress | Skill is being written — not ready for use |
| 📋 planned | Skill is on the roadmap — does not exist yet |

---

## Universal Story Chain

The framework follows a universal chain for moving from epic to implementation:

WBS Epic ↓ /decompose-wbs-epic Stories grouped under WBS parents ↓ /ears-ac Story + AC (EARS house style) ↓ /story-map-per-epic Story map ↓ /jira-split Jira ticket structure + subtasks ↓ /jira-fill Story + AC written into Jira tickets

Each step is a separate skill. The implementation subtask split (BE/FE/QA) is handled by **/jira-split**, not hardcoded elsewhere.
