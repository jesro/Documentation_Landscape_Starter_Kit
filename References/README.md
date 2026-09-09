# Documentation Toolkit — README

## The 4 files

| File | Purpose | Where it lives |
|---|---|---|
| `blueprint.md` | Master routing system — classify content and decide where it goes | `KnowledgeBase/08_References/` |
| `blueprint-integration-final.md` | Addendum — 3-dimension framing + full ADR status lifecycle | `KnowledgeBase/08_References/` |
| `adr-extraction-prompt.md` | Prompt to pull real ADRs out of a finished conversation | `KnowledgeBase/08_References/` |
| `ADR-INDEX-template.md` | Blank index — copy (not move) into each decisions folder | Copied per-folder as needed |

## Storage (once)
Save all 4 in `KnowledgeBase/08_References/`. That's their permanent
home. Never move them after this.

## Live use — per folder
Copy `ADR-INDEX-template.md` into each place you're accumulating
decisions, e.g. `KnowledgeBase/05_Decisions/ADR-INDEX.md`,
`AIVideoEditor/08_ADRs/ADR-INDEX.md`. Fill in rows as ADRs land there.

## Per-conversation use — two phases, kept separate

**Phase 1 — the discussion.** Talk normally. No blueprint files pasted
in. No priming, no classification mode, full exploratory depth.

**Phase 2 — extraction, afterward.**
- **Preferred:** open a fresh conversation. Paste the transcript plus
  `blueprint.md` + `adr-extraction-prompt.md` together, ask it to
  extract. Keeps the original thread uncontaminated.
- **Acceptable only if that thread is finished:** paste
  `blueprint.md` + `adr-extraction-prompt.md` as the last message in
  the same conversation.

**Never:** paste `blueprint.md` at the *start* of a conversation, or
load it into persistent Project/custom instructions that apply to every
chat. Priming before the thinking happens shrinks responses and steers
the discussion toward "which bucket does this fit" instead of letting
the idea develop freely.

## Minimum ritual per session
1. Discuss freely, blueprint-free.
2. When done: new chat (preferred) or last message → paste
   `blueprint.md` + `adr-extraction-prompt.md` → get ADRs → file per
   Step 2/3 of the blueprint → update the relevant `ADR-INDEX.md`.

---
For background on how documentation practices map across experience
levels, see `documentation-maturity-landscape.md` — reference material
only, not a checklist to work through.
