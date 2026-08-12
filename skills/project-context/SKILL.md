---
name: project-context
description: "Generate `01_project_context.md` for Project Knowledge from kickoff notes, PM messages, WBS fragments, onboarding notes, transcripts, or free-text project descriptions. Use at the start of a new project or when onboarding into an existing one to capture the project summary, constraints, risks, identifiers, the Project Knowledge source map, roles, the conflict-resolution rule, and conventions. This is the delivery-context file, not a PM project charter. Ask up to 3 targeted questions only when the project summary or key constraints are unclear."
---

# /project-context

Generate `01_project_context.md` — the delivery-context file for Project Knowledge. It captures how the delivery is set up (summary, constraints, risks, identifiers) and how its knowledge is organised (source map, roles, the rule for which file wins in a conflict, and reference conventions). This is not a PM project charter — no business-case or success-criteria framing.

## Inputs

Any combination of:
- Kickoff notes, PM Slack messages, free-text project description
- Scope & Vision document
- WBS (epic / scope structure)
- Architectural diagrams (uploaded as images)
- The other Project Knowledge files, if they exist — to build the Source Map and the Conflict Resolution Rule

## Process

### 1. Parse the input

Extract, if present:

| Field | Look for |
|---|---|
| Project summary | Product, client, domain, why this build, delivery model, MVP target, the lifecycle the team delivers |
| Constraints | Launch date, budget model, planning phase, resourcing, time zones, sprint cadence, SLAs, compliance |
| Risks | Explicit risks or red flags, with impact |
| Identifiers | Codename, Jira, docs tool, Figma, Slack, repo, staging URLs |
| Source Map | Each Project Knowledge file: logical name, actual filename, origin, trust level, notes |
| Roles | Canonical role names, plus any client-approved naming and the mapping from original labels |
| Conflict Resolution | Which file is the source of truth, and how conflicts between files are resolved |
| Conventions | Reference formats — WBS rows, source citations, story references, `proposed`/`TBD` tags |

### 2. Identify critical gaps

Before generating, verify the project summary and key constraints are clear enough to write factually. If either is missing or too vague, ask a maximum of 3 targeted questions. Do not invent missing facts.

### 3. Generate the document

Use the template below. The **Conflict Resolution Rule** and **Conventions** are framework standards — reproduce them as written; only add a project-specific point or adjust one where the project genuinely deviates. Everything in `[brackets]` is a project value to fill in or mark `TBD`.

```markdown
# Project Context — [Project Name]
_Last updated: [date]_

## Project
[2-4 sentences: what the product is, who the client is, the domain, why this build, delivery model, MVP target, and what the team delivers end to end.]

## Key Constraints
- [launch date / milestone]
- [budget model + any overrun process pointer]
- [planning phase + allocations]
- [resourcing — team and join dates]
- [time zones and effective overlap]
- [sprint cadence + ceremony days]
- [performance SLAs]
- [compliance obligations]

## Risks
| Risk | Impact | Notes |
|---|---|---|
| [risk] | High / Med / Low | [mitigation or open question] |

## Project Identifiers
| Tool | Value |
|---|---|
| Project codename | [codename] |
| Jira project | [instance / key] |
| Docs | [space / teamspace] |
| Figma | [org / plan] |
| Slack | [channel] |
| GitHub repo | [repo or TBD] |
| Staging / QA URLs | [URLs or TBD] |

## Project Knowledge — Source Map
| Logical name | Actual file in Project Knowledge | Origin | Trust Level | Notes |
|---|---|---|---|---|
| Product Context | [filename] | [origin] | Primary source of truth for product | Full functional scope, roles, permissions, glossary. First reference for any product question. |
| Project Context | [filename] | [origin] | Delivery context | This file. Delivery-side constraints, risks, identifiers, source map, conventions. |
| Stakeholders | [filename] | [origin] | Baseline | Roles, decision authority, contacts, RACI. |
| Tech Context | [filename] | [origin] | Baseline | Stack, integrations, architecture, domain model, technical constraints. |
| Standards | [filename] | [origin] | Baseline | Story format, EARS AC, DoR, DoD, task split, change control. |
| WBS | [filename] | [origin] | Scope baseline | Scope baseline; source for the WBS row numbers cited in the Product Context. |

## Roles [(client-approved naming, session / date if any)]
[Canonical role names, with a mapping note from any original / internal labels used in source artifacts.]

### Conflict Resolution Rule
1. **Product Context is the canonical source** for product, roles, permissions, glossary, and scope. In conflict with any other file — Product Context wins.
2. **WBS row citations in Product Context** take precedence over any narrative interpretation.
3. **Delivery-side files** (Stakeholders, Tech Context, Standards) are authoritative within their domain (team, tech stack, process). They do not override Product Context for product decisions.
4. **New decisions** from elicitations or client communications are added to Product Context first, then propagated to delivery files if needed.
5. WBS ↔ PC discrepancies are surfaced to the BA before applying — never reconciled silently. Precedence (points 1–2) decides the outcome; this point governs the procedure.
6. **Engineering / stack / data-model facts**: the engineering technical specification is canonical; the Tech Context file is its BA-facing reconciled digest. When they disagree on an engineering fact, the tech spec wins and triggers a Tech Context reconcile pass (new ADR · model change · epic kickoff). Product decisions still follow Product Context (point 1): where the tech spec and Product Context conflict on a product decision, PC wins and the divergence is surfaced to the BA, never reconciled silently.

### Conventions
- **WBS row references**: cited as `R<number>` (e.g. `R152`, `R74`). Numbers are stable within a WBS version; if WBS is re-baselined, references must be reviewed.
- **Source citations in Product Context**: `Sx transcript HH:MM:SS` or `Sx §<section>`, where the sources are listed in the Product Context source map. These sources are inputs to BA synthesis, NOT files in Project Knowledge — Project Knowledge contains synthesised outputs only.
- **Story references**: by title, not ordinal number — numbers drift on renumbering.
- **`proposed` / `TBD` tags**: any AC / requirement element tagged proposed or TBD must have a concrete Open Question whose answer clears the tag; no orphan tags without an OQ.
- **Dates**: ISO `YYYY-MM-DD` in artifacts and changelog.
- **Skill fidelity**: for any activity that has a dedicated skill, follow that skill strictly and do not deviate (decomposition → decompose-wbs-epic; etc.). **Any requirement (story + AC) MUST be produced with ears-ac — never write AC freehand, not even for a single story or a quick edit.**
- **Surfaces**: operate only on the approved surfaces defined in the Product Context; do not invent new ones. `email` is a channel, not a surface. Each story carries a one-line Surface note.
- **No source citations in client-facing requirement / AC text**: the story / AC text that goes to the tracker carries no source references. Internal traceability (WBS-AC verbatim block under the parent, PC source-map) stays separate and untouched.
- **No client personal names** in requirements (stories / AC), changelog, or any client-facing artifact (call summaries, shared OQ lists, flowcharts, design comments). The client company name is allowed. Internal-only artifacts may name freely; question formulations may name when needed.
- **Changelog trigger**: write a changelog item when an output introduces a change to existing baselined scope (Change Request) or a new feature (New Feature Request). A clarification that changes nothing baselined → no item.
- **Client questions**: written to a quality bar — one clear goal per question (know the answer you want before writing), atomic (one decision each), all filler stripped, your stance shown (understand / clarify / challenge), formed from every angle (user / admin / system), ordered most-blocking-first, and the full set surfaced at once, not drip-fed. Full rules live in elicitation-prep / open-questions-per-epic.
```

### 4. Add BA review note

After the generated document, append:

```markdown
Review before adding to Project Knowledge:
- [ ] TBD fields to resolve
- [ ] Source Map — confirm the actual filenames
- [ ] Identifiers — fill in if missing
```

## Rules

- If a field is not present in the input, write `TBD`.
- Do not invent delivery model, risks, roles, or identifiers.
- Do not use generic filler text.
- Do not document communication cadence or governance here — those belong in separate skills (`ba-communication-plan`, `ba-governance`).
- This is the delivery-context file, not a PM charter — no business-case, goals, or success-criteria framing.

## Handling large inputs

- Scope & Vision can be 30-100+ pages. Do NOT copy the full S&V text into the file.
- Extract only what belongs in the project context: the project summary, constraints, risks, identifiers.
- WBS: extract the epic list / phase structure for scope framing, not stories.
- If a source is ambiguous or contradictory, flag with `[TBD — clarify with PM / client]`; do not paraphrase to hide uncertainty.

## Output

Save as `01_project_context.md`.

## Update trigger

Regenerate or revise this file when:
- scope changes significantly
- a new delivery stream appears
- a major constraint changes
- a Project Knowledge file is added or renamed (update the Source Map)
