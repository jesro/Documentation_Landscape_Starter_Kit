# Full Documentation Landscape — Starter Kit

A practical documentation system covering the complete landscape defined in the accompanying
"Full Documentation Landscape for Software/Architecture Work".

## Core model

Keep three dimensions separate:

1. **Artifact type** — what the document is (ADR, RFC, HLD, PoC, runbook, etc.)
2. **Methodology/framework** — how it is structured (MADR, arc42, TOGAF, C4, 4+1, etc.)
3. **Lifecycle stage** — how long it lives:
   - Ephemeral
   - Temporary / evidence-producing
   - Long-lived / current
   - Historical

A single artifact can have all three dimensions. Example:

> ADR (artifact type) + MADR (methodology) + Active (lifecycle).

Organize folders by **kind of knowledge**, not by methodology.

## Recommended flow

```text
Conversation
  -> Question / Problem
  -> Research / Spike / PoC
  -> Options weighed
  -> Design discussion / Proposal
  -> Decision
  -> ADR
  -> Implementation
  -> Architecture / Design / Code / Runbook
  -> Change
  -> New ADR
```

Not every stage requires a permanent artifact.

## Core recommendation

| Need | Starting format |
|---|---|
| Capture discussion | Plain Markdown |
| Investigate unknown | Research / Spike |
| Compare options | RFC-style design proposal |
| Make architectural commitment | MADR |
| Describe whole system | arc42 + C4 |
| Describe feature implementation | HLD / LLD |
| Track problem | Risk / debt record |
| Operate system | Runbook / playbook |
| Record major change | Migration / change record |
| Preserve history | Original artifact + supersession links |

## Folder model

```text
KnowledgeBase/
├── 01_Context/
├── 02_Requirements/
├── 03_Architecture/
├── 04_Decisions/
├── 05_Design/
├── 06_Research/
├── 07_Risks/
├── 08_Operations/
├── 09_Changes/
├── 10_Conversations/
├── 11_References/
├── 12_Glossary/
├── 13_Traceability/
└── 14_Archive/          # optional; add when active navigation becomes cluttered
```

## Status principle

- Current documentation describes what is true now.
- Decision documentation explains why it became true.
- Historical documentation explains what used to be true and how it changed.

Do not delete superseded ADRs merely because they are no longer current.
