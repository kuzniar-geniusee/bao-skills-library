# Create System Prompt

A prompt for generating a project's System Prompt (Project Instructions) from `system-prompt-template`.

## What it does

Takes a description of your project plus its Project Knowledge files, and fills the `system-prompt-template` — keeping the generic framework layer (Language, Style, Behavior, Modes, Approval, Anti-hallucination, Verify-facts) as written, and replacing the project layer (role intro, glossary, project context, scope structure, Project Knowledge files) with your project's specifics.

## How to use

Paste the prompt below into a chat that has `system-prompt-template` and your project sources available (Product Context / WBS / Scope & Vision / kickoff notes, if they exist).

## Prompt

```
Generate the System Prompt for this project by filling `system-prompt-template`.

Rules:
- Keep the generic layer verbatim: Style, Behavior, Think from the user first, the Modes framework, Approval before action, Anti-hallucination, Verify project facts. Do not reword these.
- Replace the project layer with this project's specifics:
  - Role intro — project name, codename, delivery org, one-line description (what is built, for which client, on which stack).
  - Language — set the primary language and list the project glossary / contract terms that must never be translated.
  - Project context — client, contacts and their decision areas, delivery team, target/milestone, sprint cadence, scale, business model, key discovery decision, tools.
  - Scope structure — delivery phases, major MVP epics, explicit out-of-scope, from the WBS.
  - Project Knowledge files — the actual files in this project's Project Knowledge, one line each, with the WBS sheet/columns/path.
- Resolve the tool placeholders `[tracker]` and `[docs]` to this project's actual tools (or leave them if not yet decided).
- Anything unknown → write TBD and flag it. Do not invent contacts, dates, scale, or scope.

Project sources:
[paste kickoff notes / Scope & Vision / point to the Product Context and WBS in Project Knowledge]

Output the finished System Prompt as plain text, ready to paste into Project Instructions.
```

## Notes

- The output goes into the project's **Project Instructions** field, not into Project Knowledge — it is the operating contract, not a knowledge file.
- Revisit it when scope, the team, tools, or the mode set change.
