---
name: confluence-page-structure
description: "Create the empty Confluence page hierarchy for one epic — a parent page plus child pages, one per specification section, ready for the BA to fill. Executor: the action is creating the pages in Confluence via MCP; it does NOT write content into them (that is done by hand or by the generator skills). Derives which optional sections to include (Integrations/API, Data, NFRs) from the Product Context — a section the epic does not touch is omitted. Shows the planned tree for approval, then creates on 'ok'; if MCP is unavailable, hands the BA the tree as markdown to create manually. Trigger: 'створи структуру сторінок для епіку', 'зроби каркас спеки в Confluence', 'confluence structure for [epic]', 'set up the spec pages'."
---

# /confluence-page-structure

## What it does

Creates the empty page skeleton for an epic's specification in Confluence: one parent page for the epic and a child page per section (Overview, Scope, User Stories, …). Pages are created empty — heading plus a one-line placeholder only. Filling them is a separate step, by hand or by the generator skills.

This is to Confluence what `jira-split` is to Jira: it builds the structure, it does not write the content.

## When to use

- Project setup, or early on an epic, before specification work begins.
- When the epic needs a home in Confluence for its spec, review, and open questions.
- Not for writing content into the pages, and not for Jira (that is `jira-split`).

## Inputs

- The epic — its name and scope, from WBS / Product Context.
- Product Context — to decide which optional sections apply to this epic.
- Confluence target — the space key and the parent page under which to create the epic tree.

If the target space or parent page is not given, ask the BA before creating anything.

## Section set

Default child pages under the epic parent:

- Overview
- Goals
- Scope (In / Out of scope)
- User Stories
- Acceptance Criteria
- Open Questions
- Traceability

Conditional — include only when the Product Context shows the epic touches it:

- Integrations & API — if the epic has external integrations
- Data — if the epic is data-heavy (entities, dictionaries)
- NFRs — if the epic has notable non-functional requirements

A section the epic does not touch is omitted — do not create empty noise.

## Process

1. Read the epic scope from WBS / Product Context; read the Product Context to determine which conditional sections apply.
2. Build the planned tree: epic parent page → child pages (default set plus any applicable conditional sections).
3. **Show the planned tree to the BA and wait for `ok`** before creating anything.
4. On approval, create via Atlassian MCP:
   - a parent page `[Epic name] — Specification` under the given parent page;
   - one child page per section, each containing only its heading and a one-line `> Fill: [what goes here]` placeholder.
5. Return the parent link and the parent → children map.

## Output

- Created Confluence pages (parent plus children), with links.
- A parent → children map (page titles and links) for reference.

## MCP unavailable fallback

If Atlassian MCP is not accessible:

1. Output the planned tree as a markdown heading hierarchy.
2. Note: "MCP unavailable — create these pages in Confluence manually."

The methodology — which sections, in what order — is delivered regardless of tool access.

## What NOT to do

- Do not write specification content into the pages — they are created empty. Content comes from the BA or the generator skills (`decompose-wbs-epic`, `ears-ac`, and so on).
- Do not create sections the epic does not touch.
- Do not create anything before the BA approves the planned tree.
- Do not touch Jira — ticket structure is `jira-split`.

## Relation to other skills

- `jira-split` — the Jira counterpart: ticket structure for the same epic.
- `decompose-wbs-epic`, `ears-ac` — produce the content that later fills these pages.
- Product Context — the source that decides which sections apply.

## Rules

- Structure only, never content.
- Approval gate before any MCP write.
- Conditional sections are included only on Product Context evidence — never assumed.
