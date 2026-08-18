---
name: rma-generation
description: "Generate a Requirements Management Approach (RMA) document from `01_project_context.md`, `governance.md`, methodology, and tool set. Use during project setup or onboarding to formalize requirements lifecycle, traceability approach, attributes, and tooling."
---

# /rma-generation

## What it does

Generates a Requirements Management Approach document for a delivery project.
Structures project context, governance rules, and tool configuration into a formal RMA that covers the requirements lifecycle, traceability, attributes, and tool access.

Use when: project setup or onboarding, before the first refinement session.

## Inputs

Primary (read from Project Knowledge or pasted):
- `01_project_context.md` — project name, methodology, team, constraints
- `governance.md` — prioritization, approvals, change control, DoR/DoD

Secondary (ask BA if not found in primary):
- Methodology: Scrum / Kanban / hybrid
- Any additional tools (Miro, Figma, Google Drive, etc.)

## Source priority

1. Explicit BA input for the current session — overrides everything
2. `governance.md` — change control, approvals, prioritization
3. `01_project_context.md` — project name, team, constraints
4. Geniusee BA defaults — fallback for unspecified items, flag as default

## Process

### Step 1 — Gather inputs

Read `01_project_context.md` and `governance.md` from Project Knowledge.
Extract:
- Project name
- Methodology (Scrum / Kanban)
- Team roles (BA, PM, PO, dev, QA)
- Tool set ([execution tool] + [documentation tool] + any additional tools)
- Change control approach
- Prioritization and approval approach

Present summary to BA before writing:

```
Inputs found:
- Project: [name]
- Methodology: [Scrum / Kanban / TBD]
- Team roles: [list]
- Tools confirmed: [execution tool], [documentation tool], [others if any]

Gaps — need BA input:
- [list of missing values]

Proceed? (yes / provide context)
```

### Step 2 — Generate document section by section

Do not output all sections at once. Generate, then continue.

### Step 3 — Summary

```
✅ RMA document generated.

Sections with TBD content (requires BA follow-up):
- [list]

Suggested next step: share with PM / PO for alignment before first refinement.
```

---

## Output template

```markdown
# Requirements Management Approach — [Project Name]

_Version: 1.0 | Author: [BA name] | Date: [date] | Status: Draft_

---

## 1. Description

Requirements management is an iterative process aimed at defining business,
functional, and non-functional requirements to design, develop, implement,
and maintain a product throughout its lifecycle.

This document formalizes how requirements are managed on [Project Name]:
stages, activities, responsible roles, tools, and traceability approach.

**Principles:**
- Transparency in the current requirements status
- Quick access to requirements and their attributes
- Clear understanding of requirements processing at every stage

---

## 2. Requirements Management Process

**Methodology:** [Scrum / Kanban / Hybrid]

### Stage 1 — Initializing

New requirements are identified, added to the backlog, and get basic attributes.

| Activity | Responsible | Tool |
|---|---|---|
| Identify business needs | BA, PO | [execution tool] (backlog) |
| Add to backlog | BA | [execution tool] |
| Assign priority and source | BA | [execution tool] (fields) |
| Initial conflict resolution | BA, PO, PM | [documentation tool] (open questions log) |

### Stage 2 — Middle (iterative)

Requirements are elicited, specified, prioritized, estimated, approved, developed, and tested.

| Activity | Responsible | Tool |
|---|---|---|
| Elicitation (interviews, workshops) | BA | [documentation tool] (notes), Miro (if applicable) |
| Specification (user stories, AC) | BA | [documentation tool] |
| Prioritization | BA, PO, PM | [execution tool] (ranking / fields) |
| Estimation | Dev team | [execution tool] |
| Approval | PO / Client | [documentation tool] (comments) / Slack |
| Development | Dev team | [execution tool] (tasks) |
| Testing | QA | [execution tool] (subtasks) |

### Stage 3 — Finalizing

Requirements are completed, released, demonstrated, and closed or transitioned to support.

| Activity | Responsible | Tool |
|---|---|---|
| Mark requirement as Done | BA | [execution tool] (status → Done) |
| Final UAT validation | QA, PO | [execution tool] |
| Requirement retirement or archiving | BA | [documentation tool] (page archive) |
| Retrospective input | BA, PM | TBD |

---

## 3. Requirements Traceability

**Responsible:** Business Analyst

**When:** requirements must be traced before grooming, no later than sprint planning.

### Traceability in [execution tool]

Requirements (type = Story / Task) are linked to:

| Link type | Target |
|---|---|
| Subtasks | Development subtasks (BE / FE / DevOps) |
| Subtasks | QA subtasks |
| Dependencies | Blocking / Blocked-by tasks |
| Custom field | Epic / Feature group |
| Attachments / Description links | [documentation tool] specification page |

### Traceability in [documentation tool]

Each requirement page in [documentation tool] links to:

| Link type | Target |
|---|---|
| Relation | Parent epic page |
| Relation | Design (Figma / Miro link) |
| Relation | [execution tool] task URL |
| Inline reference | Related requirements ([documentation tool] page links) |

### Dependency types used

| Type | Meaning |
|---|---|
| Blocks / Blocked by | Cannot be started until predecessor is done |
| Relates to | Informational connection, no sequence constraint |
| Duplicates | Same requirement specified elsewhere — consolidate |

---

## 4. Information Management Approach

The BA is accountable for all business analysis information management.

Requirements and designs are stored and accessed as follows:

| Purpose | Tool | Location |
|---|---|---|
| Atomic requirements (stories, AC) | [execution tool] | [Project name] workspace → [Project link] |
| Descriptive documentation (BRD, RMA, specs) | [documentation tool] | [[documentation tool] space link] |
| Visual artifacts (process flows, mind maps) | Miro | [TBD — add board link] |
| Design references | Figma | [TBD — add Figma link] |
| File storage | Google Drive | [TBD — add Drive link] |

Access to all tools is granted by the PM at project start.
The BA maintains the [documentation tool] documentation space as the single source of truth for requirements.

---

## 5. Requirements Attributes

| Attribute | Description | Where managed |
|---|---|---|
| Absolute reference | Unique identifier. Not reused if requirement moves or changes. | [execution tool] task ID (auto) |
| Author | BA responsible for the requirement. | [execution tool] (Assignee field) |
| Complexity | Difficulty of implementation. | [execution tool] (custom field: Story Points / T-shirt size) |
| Ownership | Stakeholder who owns the business need. | [documentation tool] (requirement page — Owner field) |
| Priority | Relative importance or implementation sequence. | [execution tool] (Priority field) |
| Source | Origin of the requirement. | [documentation tool] (requirement page — Source field) |
| Stability | Maturity of the requirement. | [documentation tool] (Status field: Draft / Stable / Approved) |
| Status | Current state of the requirement. | [execution tool] (task status) |
| Urgency | How soon the requirement is needed. | [execution tool] (Due date) |
| Dependencies | Horizontal and vertical connections. | [execution tool] (Dependencies / Blocking links) |

---

## 6. Requirements Management Tools

| Tool | Purpose | Access |
|---|---|---|
| [execution tool] | Atomic requirements as tasks/stories. Execution tracking, status, dependencies, subtasks. | [[execution tool] workspace link — TBD] |
| [documentation tool] | Descriptive documentation: BRD, RMA, specs, meeting notes, open questions log, glossary. | [[documentation tool] space link — TBD] |
| Miro | Visual artifacts: process flows, mind maps, story maps, discovery boards. | [Miro board link — TBD] |
| Figma | UI designs and wireframes linked to requirements. | [TBD] |
| Google Drive | File storage, exports, shared assets. | [TBD] |
| Slack | Asynchronous communication, approvals, change notifications. | [TBD — project channel] |

---

## 7. Change Control Process

Changes to requirements are managed per the BA Governance Approach (`governance.md`).

Summary:

| Change timing | Risk | Process |
|---|---|---|
| Before grooming | Low | BA updates spec in [documentation tool], notifies in Slack |
| After grooming, before sprint | Medium | Re-elicitation, re-estimation, team re-confirms DoR |
| During sprint | High | CR label in [execution tool], no sprint scope change unless critical blocker |
| Post-release (delivered feature) | High | New [execution tool] task, full BA process, linked to original |

---

## 8. Open Questions

| # | Question | Owner | Target date |
|---|---|---|---|
| 1 | [execution tool] workspace link — confirm access for BA | PM | TBD |
| 2 | [documentation tool] space structure — confirm parent page for RMA | BA / PM | TBD |
| 3 | Miro board setup — confirm link and password | PM | TBD |
| 4 | Figma access for BA — confirm link | PM | TBD |
| 5 | [execution tool] custom fields — confirm Story Points / T-shirt size field exists | BA / PM | TBD |
```

---

## Rules

- Do not invent tool links, workspace names, or stakeholder names — use TBD
- If methodology is unknown, generate Scrum version and flag it as default
- Do not include BPMN diagrams in text output — note "diagram TBD, to be added in Miro"
- Change control section must reference `governance.md`, not duplicate it
- Attributes table must reflect [execution tool] + [documentation tool] reality — not Jira fields
- All TBD items must be listed explicitly in Step 5 summary
