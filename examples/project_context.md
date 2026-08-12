# Project Context — FitFlow (Wellspring Studios)
_Last updated: 2026-03-12_

> Example file — a filled `01_project_context.md` for a fictional project (FitFlow, client Wellspring Studios), to show what the `/project-context` skill produces. The **Conflict Resolution Rule** and **Conventions** are framework standards (reproduced as the skill generates them); everything else is project-specific and would be replaced per project.

## Project

FitFlow is a custom multi-tenant SaaS platform for Wellspring Studios, a US operator of boutique fitness studios (PST). It replaces a patchwork of a legacy booking tool plus spreadsheets, which hit their limits at ~40 locations / 60,000 members (scheduling conflicts, no cross-location reporting, manual billing). The custom-build path was chosen during Discovery (over Mindbody and a Vagaro-based setup) for the multi-location hierarchy and white-label needs. Delivery model is T&M with a fixed MVP target of Q3 2026 (September). Geniusee delivers the full lifecycle: planning ("month zero") → design → development → QA → data migration → MVP launch to a pilot set of studios.

## Key Constraints

- **MVP launch**: end of September 2026 (exact date TBD) — must land before the Q4 membership-renewal peak.
- **Budget**: T&M with a defined cap. SOW overrun process is defined in `04_standards.md` §8.
- **Planning phase (Month 0)**: ~1 month. BA full-time, UX 80h/month, SA 80h/month (SA likely ramps off after Month 0).
- **Resourcing**: BE x2, FE x2, QA x1, DevOps x1. Allocations / join dates TBD.
- **Time zones**: client PST (GMT−8); delivery team GMT+2. Effective overlap is narrow — afternoons client-side.
- **Sprints**: 2-week. Ceremonies Tue/Thu.
- **Performance SLAs**: static ≤3s, operational ≤5s, reporting ≤10s; API 500ms target; 99% uptime. Maintenance windows off-hours PST.
- **Compliance**: ADA / WCAG AA, PCI-DSS (payments), CCPA.

## Risks

| Risk | Impact | Notes |
|---|---|---|
| Migration from legacy booking tool + spreadsheets | High | 60k members / 40 locations, class history, active membership contracts. Risk of data loss / billing-continuity gaps. |
| Payments under PCI scope | Med | Card data must be tokenized via the provider; nothing stored in-app. Requires early validation with the SA. |
| Multi-location hierarchy not off-the-shelf | Med | Justification for the custom build, but requires early validation with the client. |
| Third-party dependency downtime (Stripe, Twilio, Postmark) | Med | Twilio is the sole SMS-reminder provider — no fallback. |
| Client-side decision bandwidth | Med | Single product owner client-side; limits sync windows for scope decisions. |

## Project Identifiers

| Tool | Value |
|---|---|
| Project codename | FitFlow |
| Jira project | Internal delivery Jira instance. Client PO has an account via delivery-org email. |
| Docs | Confluence space — URL TBD |
| Figma | Client-owned organization account, Professional plan. |
| Slack | Shared channel (client + delivery). |
| GitHub repo | TBD |
| Staging / QA URLs | TBD (environments not provisioned) |

## Project Knowledge — Source Map

| Logical name | Actual file in Project Knowledge | Origin | Trust Level | Notes |
|---|---|---|---|---|
| Product Context | `product_context.md` | BA synthesis — all primary sources | Primary source of truth for product | Full functional scope, roles, permissions, glossary. First reference for any product question. |
| Project Context | `01_project_context.md` | BA synthesis — delivery | Delivery context | This file. Delivery-side constraints, risks, identifiers, source map, conventions. |
| Stakeholders | `02_stakeholders.md` | BA synthesis — delivery | Baseline | Roles, decision authority, contacts, RACI. |
| Tech Context | `03_tech_context.md` | BA synthesis — delivery, reconciled against the engineering tech spec | Baseline | Stack, integrations, architecture, domain model, technical constraints. |
| Standards | `04_standards.md` | BA synthesis — delivery | Baseline | Story format, EARS AC, DoR, DoD, task split, change control. |
| WBS | `WBS.xlsx` | Delivery WBS, confirmed by the client | Scope baseline | Source for the WBS row numbers cited in the Product Context. |

## Roles (client-approved naming)

Owner (top tier — the studio-network account holder) · Studio Manager (runs one location) · Trainer (delivers classes, manages own schedule) · Member (books and attends classes). When reading source artifacts, expect the original internal labels (e.g. "admin", "staff") and map them with the names above.

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
