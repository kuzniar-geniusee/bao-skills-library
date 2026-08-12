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

Use the template below. Mark unknown values as `TBD`.

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
| Product Context | [filename] | [origin] | Primary source of truth for product | [what it holds] |
| Project Context | [filename] | [origin] | Delivery context | This file. |
| Stakeholders | [filename] | [origin] | Baseline | [roles, RACI] |
| Tech Context | [filename] | [origin] | Baseline | [stack, integrations] |
| Standards | [filename] | [origin] | Baseline | [story format, DoR / DoD] |
| WBS | [filename] | [origin] | Scope baseline | [source for row numbers] |

## Roles [(client-approved naming, session / date if any)]
[Canonical role names, with a mapping note from any original / internal labels used in source artifacts.]

### Conflict Resolution Rule
1. **[Primary file] is the canonical source** for [its domain]. In conflict with any other file — it wins.
2. [WBS row citations take precedence over narrative interpretation.]
3. [Delivery-side files are authoritative within their own domain and do not override the primary for product decisions.]
4. [New decisions are added to the primary first, then propagated to delivery files.]
5. [WBS <-> PC discrepancies are surfaced to the BA before applying — never reconciled silently.]

### Conventions
- **WBS row references**: [format, e.g. `R<number>`; note that numbers are stable within a WBS version and must be reviewed on re-baseline]
- **Source citations**: [format, e.g. `Sx §<section>`; note these are inputs to BA synthesis, not files in Project Knowledge]
- **Story references**: [by title, not ordinal number]
- **`proposed` / `TBD` tags**: [each must have a matching Open Question that clears the tag]
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
