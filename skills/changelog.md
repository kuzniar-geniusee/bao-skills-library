---
name: changelog
description: "Write a single change-log item as a ready-to-paste horizontal row matching the project's live Change Log sheet. Trigger ONLY when the BA explicitly asks for it — e.g. 'напиши айтем в чейнджлог', 'write a changelog item', 'додай це в change log'. Do NOT trigger merely because a decision or source arrived. Fills content columns A–M (A Change_ID as a placeholder, L Requestor as [Client]/Geniusee, K Jira ticket = TBD); leaves Responsible, Status, Approval Date, Jira, and all effort columns untouched. A Change Request reuses the current baseline story+AC verbatim (Jira/Confluence if the story is described there, else WBS) and marks the delta (strike removed requirements, list new ones). Delivers the item as a horizontal markdown row in chat. Does not edit the Product Context — that is pc-update."
---

# /changelog

Write one change-log item from a decided change, as a row matching the project's live **Change Log** sheet. Output is a **horizontal** markdown row the BA pastes in. The skill writes content columns only and never touches process-metadata or estimation columns.

## Trigger gate — read first

Only produce a change-log item when the BA explicitly asks for one ("напиши айтем в чейнджлог", "write a changelog item"). A decision or source arriving is not the trigger — writing the item is a deliberate step the BA invokes. When unsure, ask.

## Inputs

- The decided change — from a call summary, client answer, dev/design sync, or stated decision.
- The **baseline** — for a Change Request: the refined story+AC from Jira/Confluence if the story is already described there, otherwise the WBS row (see Baseline resolution).
- The existing change log — to match its numbered AC style.

## Live column layout

The Change Log sheet columns are:

`A Change_ID · B Date · C Source · D Epic Name · E Task/US Description · F Acceptance Criteria · G Phase · H Comments / Questions · I Responsible · J Type · K Jira ticket · L Requestor · M Status · N Approval Date · O Jira · P onward Effort (PERT per role: Back-End / Front-End / QA / UX-UI / BA / DevOps / PM / TOTAL)`

## Columns the skill writes

| Col | Name | Content |
|---|---|---|
| A | Change_ID | Placeholder `Change-NN` — **do not auto-number**. The BA assigns the real sequential number on paste. |
| B | Date | Date of the decision / call the change came from. `TBD` if not provided — do not invent. |
| C | Source | Where it came from (call, refinement, dev/design sync, client message, Confluence, WBS comment…). `TBD` if unknown. |
| D | Epic Name | The epic from scope. |
| E | Task / US Description | The user story (see Type logic + Baseline resolution). |
| F | Acceptance Criteria | The AC, numbered to match the change log's plain-numbered style — **not EARS**. |
| G | Phase | `MVP` or `Future Phase`. |
| H | Comments / Questions | Short description of the change; **and for a Change Request, the baseline used** — e.g. `Baseline: Jira PROJ-632` or `Baseline: WBS R40 (generic, no US)`. |
| J | Type | `New Feature Request` or `Change Request` — these two values only. |
| K | Jira ticket | `TBD`. |
| L | Requestor | `[Client]` (the client's name) if the client requested the change; `Geniusee` if it was initiated internally (our dev/design sync, our proposal). Infer from Source. |

**Leave blank — the skill never fills these:** `I Responsible`, `M Status`, `N Approval Date`, `O Jira`, and all effort columns (`P` onward). These are team / process / estimation metadata owned by PM and estimators.

## Type logic — this drives the whole item

### New Feature Request

No matching item existed. Write **E (story) and F (AC) from scratch** — a proper user story (`As a [role], I want [action], so that [benefit]`) and numbered AC in the change log's style. WBS is not involved. Requestor is normally `[Client]` (a client ask) unless the Source shows it originated internally.

### Change Request

An item exists and is being modified — a phase move (MVP ↔ Future Phase) and/or an AC change. The story and AC must be the **baseline text, verbatim** (see Baseline resolution). Then show the delta:

- **Phase change:** set G to the new phase; describe the move briefly in H.
- **AC change:** in column F, keep the baseline AC; **strike removed requirements** with strikethrough; add new ones under a `New requirements:` heading. In H, briefly state what changed **and** the baseline used.

## Baseline resolution (Change Request only)

The verbatim "original" is whichever baseline currently governs the story:

1. **Story already described in Jira/Confluence** (a refined story+AC exists) → baseline = **that refined text, verbatim**. Compute the delta against it.
2. **Story not yet in Jira** (only WBS) → baseline = **the WBS row, verbatim**. If the WBS row has no user story or is a generic bundled row (e.g. R40), take the WBS AC as-is and mark the story as derived.

The skill does **not** auto-detect which case. It goes by what the BA provides: a Jira key / refined text → branch 1; "not in Jira yet" / only a WBS row → branch 2. If it is unclear, ask exactly one question: **"Is this story already in Jira?"**

Always record the baseline used in **H** (e.g. `Baseline: Jira PROJ-632`, `Baseline: WBS R40 (generic, no US)`) so the delta's origin is self-documenting in the log.

## Removed-AC marking

Deliver removed requirements **struck through here in chat** (`~~text~~`). Because the change log is an **Excel** sheet, markdown tildes will not render there — so the handoff line must remind the BA to apply **Excel strikethrough formatting** to those lines on paste.

## What NOT to do

- Do not produce an item before the BA explicitly asks.
- Do not auto-number Change_ID — placeholder `Change-NN` only.
- Do not fill `I Responsible`, `M Status`, `N Approval Date`, `O Jira`, or any effort column (`P`+).
- For a Change Request, do not paraphrase the baseline story or AC — reuse verbatim and mark only the delta.
- Do not reformat AC into EARS — match the change log's numbered style.
- Do not invent Date or Source — use `TBD`.
- Do not edit the Product Context or any other artifact — this skill writes one change-log item only.
- Use canonical role names; never translate client glossary terms.

## Output

A single **horizontal** markdown row in column order **A–M**, ready to paste. Preserve empty cells for alignment (`I` and `M` blank; `K` = `TBD`); **exclude** effort columns (`P`+). Use strikethrough for removed AC requirements. End with a one-line handoff note reminding the BA to (a) assign the real `Change_ID` and (b) apply Excel strikethrough to any struck AC lines.

When E / F / H are long, they will be cramped in a horizontal cell — it is fine to repeat those three fields in full beneath the row for readability, while the row itself remains the paste-ready artifact.
