---
name: stakeholder-analysis
description: "Generate `02_stakeholders.md` from `01_project_context.md`, kickoff notes, PM messages, org charts, or free-text stakeholder descriptions. Use after the Project Charter or when onboarding onto an existing project to map internal and client stakeholders, decision authority, responsibilities, communication context, and a BA-focused RACI. Create the internal version first, keep Power/Interest for BA use only, and ask whether an external-facing version is also needed."
---

# /stakeholder-analysis

Generate `02_stakeholders.md` as the structured stakeholder map for the project. This file should support communication planning, approvals, escalation, and BA alignment.

## Inputs

Accept any of the following:
- `01_project_context.md`
- Kickoff notes
- PM message with stakeholder mentions
- Existing stakeholder list or org chart
- Free-text description of team members and client contacts

If the project has separate streams, map stakeholders per stream where relevant.

## Process

### 1. Extract stakeholders

Identify all relevant people and groups involved in the project:
- Internal team: BA, PM, dev, QA, design, tech lead
- Client-side stakeholders: PO, CTO, PM, SME, approvers, end-user reps
- Vendors or third parties when relevant

For each stakeholder, capture what is known:
- Name
- Role
- Organization
- Contact channel or email if provided
- Time zone if provided
- Responsibilities
- Decision-making authority
- Communication preferences
- Concerns, work style, or special notes if explicitly known

Group-level entries are acceptable when individuals are not known yet.

### 2. Classify influence and interest

For internal BA use only, assign:
- Power: High / Low
- Interest: High / Low

If classification is unclear, mark as `TBD` rather than guessing.

### 3. Build a BA-focused RACI

Cover these standard BA deliverables:
- Requirements specification
- Requirements approval
- Change request approval
- User acceptance testing
- Sprint demo / review

Generate a sensible default matrix based on known roles, then flag it for review.

### 4. Flag missing stakeholder data

After generation, list stakeholders where critical information is missing.
Use a short follow-up note such as:

> The following stakeholders need more information before the next client interaction: [list]. Suggest clarifying this on the next call or async.

## Output template

```markdown
# Stakeholders — [Project Name]
_Last updated: [date]_
_⚠ Internal document — Power/Interest columns for the delivery team only_

## [Client] (Client)

| Name | Role | Contact | Time Zone | P/I | Notes |
|---|---|---|---|---|---|
| [Name] | [Role] | [Slack / email] | [GMT±x] | H/H | [Decision authority, working style, availability, approvals, watch-outs] |

## [Delivery Org] (Delivery Team)

| Name | Role | Contact | Notes |
|---|---|---|---|
| [Name] | [Role] | [email] | [What they own, escalation point, availability] |

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
```

## Rules

- Do not invent names, contacts, time zones, or decision authority
- Do not assume Power/Interest when the basis is weak, use `TBD`
- Keep internal political notes out of any external-facing version
- Generate the internal version first
- If the user also needs a client-safe version, remove Power/Interest and internal concerns notes

## Output

Save as `02_stakeholders.md`.
