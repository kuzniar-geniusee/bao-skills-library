# Product Context — FitFlow (Wellspring Studios)
_Last updated: 2026-03-12_

> Example file — a **skeleton** `product_context.md` for a fictional project, to show the structure the `/pc-from-zero` skill builds (§1–§11) and the level each section is written at. This is illustrative, not a full product spec: each section shows 2–3 example entries, where a real Product Context would carry the complete detail. Section structure is standard; all content is project-specific.

## 1. Product overview

- FitFlow is a multi-tenant platform for a network of boutique fitness studios: class scheduling, memberships, trainer management, and billing across locations.
- Two audiences: studio staff (Owner, Studio Manager, Trainer) who run operations, and Members who browse and book classes.
- MVP targets a pilot set of Wellspring locations; full rollout follows after the pilot.

## 2. Users and roles

- **Owner** — the network account holder; sees all locations, billing, and cross-location reporting.
- **Studio Manager** — runs one location: schedule, staff, local members.
- **Trainer** — delivers classes, manages own availability.
- **Member** — books, attends, manages their membership and payment method.

## 3. Domain model

- Core entities: Owner, Location, Trainer, Member, Class, ClassInstance, Booking, Membership, Payment.
- A Member's Membership has a status (Active / Paused / Lapsed / Cancelled) that governs booking rights.
- A ClassInstance has capacity and an ordered Waitlist.

## 4. Functional domains

- **Scheduling** — create classes, generate recurring instances, manage capacity and waitlists.
- **Memberships** — plans, sign-up, pause/resume, renewals, cancellations.
- **Billing** — recurring membership charges, one-off class payments, refunds (via Stripe).
- **Reporting** — attendance, revenue, membership churn, per-location and network-wide.

## 5. System rules and automations

- When a ClassInstance has a cancellation, the first Member on the Waitlist is auto-promoted and notified (SMS + email).
- A Membership moves to `Lapsed` automatically after a failed renewal charge plus a grace window.
- Reminders send 24h and 2h before a booked ClassInstance.

## 6. Integrations

- **Stripe** — all payments and recurring billing (tokenized, PCI).
- **Twilio** — SMS reminders and waitlist alerts.
- **Postmark** — transactional email.
- (See Tech Context for direction, ownership, and constraints.)

## 7. Out of scope (MVP)

- Native mobile apps (MVP is responsive web).
- Per-location white-label theming.
- In-app trainer payroll.

## 8. Parallel tracks

- Data migration from the legacy booking tool runs alongside build; owned jointly by SA and client Ops.
- Brand/visual design owned by the client's designer; delivery UX consumes the approved system.

## 9. Glossary

- **ClassInstance** — a single scheduled occurrence of a Class.
- **Lapsed** — a Membership past its failed-renewal grace window.
- **Waitlist** — ordered queue for a full ClassInstance.

## 10. Source map

- S1 — Discovery workshop transcript (2026-02, scope + roles).
- S2 — Ops walkthrough (scheduling and membership rules).
- S3 — Client billing-rules document.

## 11. Permission matrix

| Action | Owner | Studio Manager | Trainer | Member |
|---|---|---|---|---|
| View network-wide reports | ✅ | — | — | — |
| Manage a location's schedule | ✅ | ✅ (own location) | — | — |
| Set own availability | ✅ | ✅ | ✅ | — |
| Book a class | — | — | — | ✅ |
