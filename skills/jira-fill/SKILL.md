---
name: jira-fill
description: "Write finalized requirements (story + AC) into Jira tickets from a Notion markdown export. Runs after jira-split has built the empty ticket structure. The BA pastes the epic's MD (all stories with their AC); the skill writes each story's story+AC into its matching ticket. If a ticket's description is non-empty, the old title+description are moved to a comment for traceability first, then the new content is written; if empty, written directly. Pure transfer — no DoR check, no flags, no interpretation. Also serves single-ticket updates when a requirement changes. Trigger when the BA says 'fill the epic', 'залий вимоги в джиру', 'fill AC into tickets', 'онови CID-XXX'."
---

# /jira-fill

## Purpose

Write finalized requirements (story + Acceptance Criteria) into Jira tickets. Runs after `jira-split` has created the empty ticket structure: the BA pastes the epic's Notion markdown (all stories with their AC), and the skill fills each story's content into its matching ticket. Also serves a single-ticket update when one requirement changes. Pure transfer of what the BA provides — no validation, no DoR check, no flagging, no rewriting.

## When to invoke

- After `jira-split` — to fill the epic's empty tickets with their story + AC.
- When a requirement already in Jira changed — to update one ticket.

## Inputs

- **Notion MD** — the epic's stories with AC, exported from Notion and pasted by the BA. May be the whole epic (many stories) or a single story.
- **Target tickets** — for an epic fill, the tickets created/renamed by `jira-split`; the skill matches each MD story to its ticket by title. For a single update, the BA gives the CID directly. The WBS↔CID link is never guessed — when a match is unclear, the skill asks rather than assuming.

## Process

For each story in the MD:

1. Read the target ticket's current state via MCP (read-only, no approval).
2. **Traceability rule:**
   - Description **non-empty** → move the current title + description into a **comment** on the ticket, then continue.
   - Description **empty** → skip the comment (a freshly split ticket has nothing prior to preserve).
3. Write the requirement into the ticket: title and description from the MD. Story + AC go into the description as given.
4. Report `Story name → Jira link`.

That is the whole skill. **No** DoR check, **no** `[DoR-MISSING]` flags, **no** field validation, **no** added structure — only what the MD contains.

## Matching MD stories to tickets

For an epic fill, match each MD story to the ticket whose title equals the story's title (the titles `jira-split` wrote from WBS column D). Show the matched plan (`MD story → CID`) before writing, and let the BA correct any pairing. Unmatched MD story or unmatched ticket → flag it, do not force a match.

## Why traceability lives here, not in jira-split

`jira-split` deliberately does not touch comments or descriptions. If both skills wrote the traceability comment, the previously-existing parent tickets would get it twice. Keeping it solely here means the comment is written exactly once, at the moment the old content is about to be overwritten, by the skill that overwrites it.

## Output

- Each target ticket's title and description set to its MD requirement.
- A traceability comment holding the prior content, only where the description had content before.
- Chat report: `Story name → Jira link` per ticket.

## MCP unavailable fallback

Print, per story: the formatted title + description (story + AC), and — if the prior description was non-empty — the prior content to paste as a comment first. The BA applies it in Jira manually.

## Behavior parameters

- Temperature low — deterministic transfer, not generation.
- Read before write; approval before write (show the match plan, then write). Read-only MCP (fetch) runs without approval.
- Anti-hallucination: write only what the MD contains. Do not add AC, fields, labels, or assignees not present in the input.

## What this skill does NOT do

- Does not check DoR or flag missing fields.
- Does not write or rewrite AC — the AC is provided final in the MD.
- Does not decide the split or create tickets — that is `jira-split`.
- Does not touch subtasks — they already exist from `jira-split`.
- Does not write back to the WBS.

## Relation to other skills

- Runs **after** `jira-split` (Split = structure, Fill = content).
- Consumes the finalized story + AC the BA refined (post `ears-ac` / `gherkin-ac` and team refinement), exported from Notion as MD.
