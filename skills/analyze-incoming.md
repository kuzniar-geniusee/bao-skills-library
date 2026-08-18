---
name: analyze-incoming
description: "Explain an incoming item and route it to the next action. Use when the BA pastes a client change-log comment, a client message, a transcript snippet, a PRD section, or a newly proposed feature and asks what it means and what to do — e.g. 'про що це і що робити', 'проаналізуй цей коментар', 'поясни цей айтем'. Cross-checks the item against the current Product Context / WBS, states the real decision at stake, and routes it (apply directly · ask the client · bring to call · no action · or whatever fits). When the route is a client question, it drafts that one question. Does NOT edit the Product Context or write the changelog itself — those are separate, explicitly-requested steps handled by pc-update and the changelog skill."
---

# /analyze-incoming

Take one incoming item and do two things: explain what it actually is and the real decision behind it, then route it to the next action. This is the front-door reasoning step that *precedes* any commit to the Product Context or changelog — it grounds the item, makes sense of it, and decides where it goes.

## What this skill is and is not

- **Is:** the analysis and routing step. Ground the item against the project, explain the decision, decide the next action.
- **Is not:** the PC commit step (→ pc-update) or the changelog write step (→ changelog skill). It does not edit the PC or the changelog. It *may* draft a single client question when that is the route, because that is a small inline action — assembling a full prioritized question set for a session is the separate, heavier elicitation-prep skill.

## Inputs

One or more incoming items, any type: client change-log comment, client Slack/board message, transcript snippet, PRD section, newly proposed feature. Plus read access to the current Product Context (and the WBS where row numbers matter).

## Process

### 1. Ground the item

Targeted cross-check against the current PC (and WBS if relevant): what does the project already say on this exact point? Is this genuinely new, already covered, a change to something decided, or a contradiction? Do not analyze in a vacuum — a wrong read here sends the item down the wrong route.

### 2. Explain the item and the decision behind it

State what the item actually is and the real problem or decision at stake — clearly and directly, in short scannable sentences: one point per sentence, no nested parentheticals, no restating the same point twice. Ground it against whatever the project already says on this point (PC section, story, WBS, design) and keep that grounding — it is the value — but say it cleanly, not as one dense clause. Do not just restate the item back verbatim; surface the meaning the BA needs to act on. Keep it as long as the item requires and no longer.

*Heavy → clean (same grounding, lighter packaging):*

- Heavy: This is an engineering decision: admins authenticate via SSO (say Okta), not a password. The PC currently leaves the admin invite-acceptance / credential mechanism as TBD (an open question in User Registration). This decision closes that TBD.
- Clean: Admins will sign in via SSO (Okta), not a password. In the PC the admin-activation mechanism is `TBD` (User Registration) — this closes it.

### 3. Route to the next action

Classify the item and say it crisply as "this is X → do Y". The routes below are the common ones; they are not a closed set — if a different action fits the item better, use it and name it.

| Route | When | Hand-off |
|---|---|---|
| **Apply directly** | A decision already exists, or it is a pure narrowing / cleanup — no client input needed | Name the commit target: PC update · changelog · board comment · requirement/AC edit. Also say whether it can be applied as-is or should still be confirmed with the client (the recurring "apply now vs bring to call" call). The commit itself happens via the matching skill on the BA's command. |
| **Ask the client** | The item raises something undecided or ambiguous; the client must rule | Draft the question itself — short, in English, addressed to the right person (the product owner for product, the tech lead for technical). Flag it if it carries scope risk. |
| **Bring to call** | Needs live discussion, multiple parties, or trade-offs | Note what to put on the agenda and why. |
| **No action** | Already covered, out of scope, or a note that only needs acknowledging | Say which, and that nothing changes. |

An item can carry more than one route (e.g. apply part directly, ask the client about the rest) — split it and route each part.

### 4. Stop at the route

End at the routing decision (plus the drafted question where the route is "ask the client"). Do not emit find/replace blocks and do not write changelog entries. If the BA then says "дай find/replace" or "запиши в changelog", that hands off to pc-update or the changelog skill.

## What NOT to do

- Do not edit the Product Context or write the changelog from this skill — analyze and route only. (Drafting a single client question is allowed; producing PC edits or changelog entries is not.)
- Do not pick a winner on a real conflict — route it to the client and draft that question.
- Do not restate the item verbatim instead of explaining it; lead with the decision at stake.
- Do not bury the grounding in one dense clause with nested parentheticals, or restate the same point twice — keep the project link (PC / story / WBS / design) but say it in short clean sentences.
- Do not invent project facts — cross-check against the PC/WBS, or mark "not defined, needs confirming".

## Output

In-chat only: a clear explanation of the item and the decision behind it, plus the route per item ("this is X → do Y", with apply-now vs confirm-with-client noted). Where the route is "ask the client", include the drafted question. No files, no PC/changelog commits.
