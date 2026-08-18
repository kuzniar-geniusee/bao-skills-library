---
name: call-summary
description: "Write a client-facing summary of an elicitation or working session from its transcript. Use when the BA asks for a meeting/call summary after a session — e.g. 'напиши саммері по дзвінку', 'саммері після елісітації', 'summary зустрічі для клієнта'. The transcript is always the input; a prepared question list and a change log are optional extra inputs. Produces a shareable markdown summary: header + overview + decisions grouped by theme + (a Q&A table only when the session ran through a prepared question list) + open items + change-log delta. Never attributes statements to a speaker, and uses canonical role names only. For an internal extract of requirements / action items, use meeting-to-requirements instead."
---

# /call-summary

Write a client-facing summary of an elicitation or working session, suitable to share with the client. Built from the session transcript, it records what was decided and what remains open, in a clean, professional, decision-focused form.

## When to use vs meeting-to-requirements

- **call-summary (this skill):** a shareable session summary for the client — decisions, Q&A, open items, change-log delta.
- **meeting-to-requirements:** an internal extract of requirements, action items, and open questions for the team. Different artifact, different audience.

## Inputs

- **Transcript — always.** The summary is built from it.
- **Prepared question list — optional.** If the session ran through one, it drives the Q&A table.
- **Change log — optional.** If relevant, it drives the change-log delta callout.

## Output

A markdown file, `call_summary_[date].md`. Shareable with the client.

### Structure

```markdown
# #[N] Elicitation ([date])
Attendees: [names + roles]
[Duration / Purpose — if known]

## Overview
[One short paragraph: what the session covered.]

## Decisions
### [Theme 1]
- [Decision as a final state, full sentence. MVP / Future tagged where relevant.]
- ...
### [Theme 2]
- ...

## Q&A
[Only when the session ran through a prepared question list.]
| Topic | Question | Assumptions | Answer | Status |
|---|---|---|---|---|
| ... | ... | ... | ... | resolved / open |

## Open items
[Numbered — what remains unresolved or awaiting client input.]
1. ...

## Change log
[Only when relevant: an explicit callout of what from this call goes to the changelog.]
```

## Section rules

- **Decisions — always.** Group by theme, each theme a bold lead-in heading, each decision a full-sentence bullet stating the *final decided state* (not the path the discussion took). Tag MVP vs Future explicitly wherever it applies. One decision per bullet.
- **Q&A — conditionally.** Include the table only when the session was structured around a prepared question list (discrete question → answer pairs). For free-form discussion sessions, omit it — the decisions section already carries the outcomes. Both can coexist when a call did both.
- **Open items — when any exist.** Number them; state what is unresolved and, where useful, that it awaits the client.
- **Change log — when relevant.** A short explicit note of which items from this call feed the changelog, so the scope trail is connected.

## Writing rules

- **No speaker attribution.** Never write who said what — no "X said", "Y confirmed", "the client noted". State every decision impersonally, as the session's outcome. This summary is shared with the client; naming who said what is out of place.
- **Verbatim only in parentheses, still unattributed.** If exact wording matters, put it in quotes inside parentheses — but never name the person who said it.
- **Canonical roles only.** Map any legacy or transcript labels (e.g. PGL, GL, SA, PSA, Super Admin, Participant) to the canonical names (System Admin, Admin, Group Owner, Group Leader, Learner). Never show legacy labels in the summary.
- **Final state, not discussion.** Record the decision reached, not the back-and-forth that produced it.
- **Professional, decision-focused tone.** Full-sentence bullets. No filler.
- **Do not invent.** Only what the transcript and provided inputs support. Mark unresolved points as TBD in Open items rather than guessing.

## Glossary terms

Never translate client glossary terms (Group, Site, Group Owner, Group Leader, Learner, Courses+, Subscriptions+, user-state names, etc.) — use them exactly as the project defines them.
