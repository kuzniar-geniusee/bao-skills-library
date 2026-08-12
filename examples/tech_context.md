# Tech Context — FitFlow (Wellspring Studios)
_Last updated: 2026-03-12_

> Example file — a filled `03_tech_context.md` for a fictional project, to show what the `/tech-context` skill produces. Section structure is standard; all values are project-specific and would be replaced per project.

## Stack

| Layer | Technology | Notes |
|---|---|---|
| Frontend | TypeScript / React | Member app (mobile-first) + manager dashboard |
| Backend | Node / NestJS | REST API, modular per domain |
| Database | PostgreSQL | Multi-tenant, row-level tenant scoping |
| Infrastructure | AWS (ECS, RDS, S3) | IaC via Terraform |
| Auth | Auth0 (OAuth / SSO) | SSO for Owners/Managers; email+password for Members |
| PM Tool | Jira — internal delivery instance | |
| Design | Figma | |

## External Integrations

| Integration | Purpose on This Project | Direction | Owner | Constraints / Notes |
|---|---|---|---|---|
| Stripe | Membership billing, one-off class payments | Bidirectional | SA | PCI — tokenized, no card data stored in-app |
| Twilio | SMS class reminders, waitlist alerts | Outbound | BE | Sole SMS provider — no fallback |
| Postmark | Transactional email (receipts, password reset) | Outbound | BE | |
| Mux | Class video hosting (on-demand library) | Bidirectional | BE | Streaming URLs signed per-request |
| Google Calendar | Trainer schedule sync | Bidirectional | BE | Optional per trainer |

## Architecture Notes

Multi-tenant SaaS with an Owner → Location → Class hierarchy. API-first: the member app and manager dashboard are separate frontends over one API. Tenant scoping is enforced at the data layer (every query carries a tenant id). Background jobs (reminders, billing runs) run on a queue.

## Domain Model & Data

Core entities: `Owner` (network account), `Location`, `Trainer`, `Member`, `Class`, `ClassInstance` (a scheduled occurrence), `Booking`, `Membership` (plan + status), `Payment`. A `Member` may hold memberships across locations of the same Owner. The authoritative model lives in the engineering tech spec; this file carries the BA-facing digest and defers to the spec on field-level detail.

## Design Constraints

Manager dashboard follows a table-plus-detail pattern (list of classes/members → drawer for detail). Member app is mobile-first, minimal steps to book. Accessibility to WCAG AA. No custom theming per location in MVP (single Wellspring brand).

## Technical Constraints

- Payment card data must never touch the app servers — Stripe Elements + tokenization only (PCI).
- Tenant data isolation is mandatory; no cross-tenant queries.
- SMS/email sends are rate-limited and must be idempotent (no double reminders).

## MVP Test Coverage

Unit tests on billing and membership-status logic (highest risk). E2E on the core booking flow (browse → book → confirm → reminder). Migration validated with a dry-run against a copy of legacy data. Load testing deferred to pre-launch.

## Open Technical Questions

- [ ] SSO provider confirmation for Owners/Managers — Auth0 vs the client's existing identity provider.
- [ ] Video hosting — Mux vs Vimeo; decision depends on the on-demand library scope in MVP.
- [ ] Data residency requirement for member PII — confirm with the client.

## Tech Glossary

| Term | Definition | Synonyms / Abbreviations | Needs Clarification |
|---|---|---|---|
| ClassInstance | A single scheduled occurrence of a Class at a time and location | Session, occurrence | No |
| Tenant | One Owner account and all its locations/data | Org | No |
| Waitlist | Ordered queue for a full ClassInstance | — | No |
