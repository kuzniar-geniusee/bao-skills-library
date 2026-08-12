# Stakeholders — FitFlow (Wellspring Studios)
_Last updated: 2026-03-12_
_⚠ Internal document — Power/Interest columns for the delivery team only_

> Example file — a filled `02_stakeholders.md` for a fictional project, to show what the `/stakeholder-analysis` skill produces. Names are fictional. The **RACI** and **Influence / Interest** blocks are framework defaults (reproduced as the skill generates them); the stakeholder tables are project-specific.

## Wellspring Studios (Client)

| Name | Role | Contact | Time Zone | P/I | Notes |
|---|---|---|---|---|---|
| Jordan Blake | Founder, Owner, **PO** | jordan@wellspring.example | PST (GMT−8) | H/H | Product vision, scope decisions, MVP sign-off, budget owner. Tue/Thu preferred. |
| Sam Rivera | Head of Operations | sam@wellspring.example | PST (GMT−8) | H/H | Day-to-day operational rules (scheduling, memberships), SME for studio workflows. Approves in the PO's absence. |
| Alex Chen | Finance Lead | alex@wellspring.example | EST (GMT−5) | H/L | Billing/payment rules, PCI sign-off. Joins milestones, not daily. |

## Geniusee (Delivery Team)

| Name | Role | Contact | Notes |
|---|---|---|---|
| M. Ivanenko | Delivery Manager | (delivery-org email) | Escalation point at client-relationship level. Not in daily delivery loop. |
| O. Petrenko | Project Manager | (delivery-org email) | Runs ceremonies, sprint planning, client sync. |
| (you) | Business Analyst | (delivery-org email) | Requirements, elicitation, specification. |
| K. Bondar | UI/UX Designer | (delivery-org email) | Flows, mockups, design system. |
| D. Melnyk | Solution Architect | (delivery-org email) | Stack, data model, integrations. Ramps off after Month 0. |

## RACI

| Deliverable | BA | PO / Client | PM | Tech Lead | Dev Team | QA |
|---|---|---|---|---|---|---|
| Requirements specification | A | C | I | C | C | C |
| Requirements approval | C | A | C | I | I | I |
| Change request approval | C | A | C | I | I | I |
| UAT | R | I | I | — | — | A |
| Sprint demo / review | R | I | I | C | C | A |

> R = Responsible, A = Accountable, C = Consulted, I = Informed. Adjust to the actual project structure.

## Influence / Interest Notes

- **High Power / High Interest** → manage closely
- **High Power / Low Interest** → keep satisfied
- **Low Power / High Interest** → keep informed
- **Low Power / Low Interest** → monitor with minimal effort
