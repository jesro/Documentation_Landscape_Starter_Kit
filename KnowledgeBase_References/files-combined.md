--- FILE: README.md ---

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

--- FILE: ADR-INDEX-template.md ---

# ADR Index (copy this into any `05_Decisions/` or `08_ADRs/` folder)

Scan this file, not the individual ADRs, when picking up work after a
gap. Only open a linked ADR if the one-line context is relevant to what
you're doing today.

| ID | Title | Status | One-line context |
|----|-------|--------|-------------------|
| | | | |

**Rule:** never edit an Accepted ADR. Write a new one and mark the old
`Superseded by ADR-XXXX` if the decision changes.

--- FILE: adr-extraction-prompt.md ---

# ADR Extraction Prompt (run at the end of any planning conversation, same session)

```
Using the Documentation & Decision Blueprint I've shared, go through this
conversation and extract durable knowledge only — do not summarize the
conversation itself.

1. Apply Step 0 (the ASR gate) to anything that looks like a decision.
   NOT ADR-worthy, even if discussed at length: which package got
   installed, a single test run, a config value that got tweaked
   (e.g. "changed temperature 0.7→0.3"), a one-off prompt tried, a
   model simply downloaded/tested without a comparison being settled.
   Those are experiments/config history, not decisions.

1A. AUTHORITY CHECK — a recommendation is not a decision.
   Do not treat an AI/assistant recommendation as a user/project
   decision. Phrases such as "I recommend", "best choice", "you
   should", "what I would build", "final verdict", or similar indicate
   a recommendation UNLESS the conversation contains explicit evidence
   the user accepted, committed to, or adopted it.

   For every candidate decision, distinguish:
   - AI/assistant recommendation
   - User/project decision
   - Decision status: Accepted / Proposed / Pending validation / Rejected

   If user acceptance can't be established from the conversation, do
   NOT create an Accepted ADR. Classify it as Proposed or Pending
   instead, or file it under Knowledge/Reference/Project Requirements
   if that fits better. Never infer acceptance merely because the user
   kept discussing the recommendation or asked follow-up questions
   about it — only explicit agreement counts.

2. Sort everything else into these buckets — only include a bucket if
   the conversation actually produced that type of content:

   - DECISIONS (passed the ASR gate AND the authority check)
   - KNOWLEDGE / REFERENCE (reusable know-how, comparisons, glossaries)
   - PROJECT REQUIREMENTS (something the app must do)
   - MODEL RECORDS (facts about a specific model: family, license,
     params, GGUF availability, RAM, strengths/weaknesses)
   - BENCHMARK / EXPERIMENT DEFINITIONS (what was tested, how, not yet
     a decision)
   - TODO / OPEN QUESTIONS (unresolved, needs a future decision)
   - REJECTED ALTERNATIVES (seriously considered, not chosen, and why)
   - PROPOSED / PENDING (recommendations discussed but not yet
     explicitly accepted — see 1A)
   - DISCARD (interesting in the moment, not durable — name it so I
     know it was seen and deliberately dropped, not missed)

3. For each DECISION, output a separate ADR using this exact template:

# ADR-XXXX: <short title>
Date: <today's date>
Status: Accepted
Source: <this conversation's date/name>
## Context
<1-3 sentences>
## Decision
<1-3 sentences>
## Consequences
<bullets, at least one real downside>
## Alternatives Considered
<bullets, only genuinely-weighed options>

For anything in PROPOSED / PENDING, use the same template but set
Status: Proposed, and skip writing an ADR number until it's accepted —
just log it as a row in the relevant ADR-INDEX.md instead.

4. For everything else, just give a one-line description per item plus
   its bucket — don't format non-decisions as ADRs.

5. For each item, say where it should be filed per Step 2/3 of the
   blueprint (platform, shared, or project — and which folder). If a
   decision isn't ready to be a full ADR yet, say "log as Pending in
   ADR-INDEX.md" instead of writing the full record.

Do not invent information. Only extract what was actually said. Number
ADRs starting from <next free number in your index>.
```

--- FILE: blueprint-integration-final.md ---

# Blueprint Integration Notes (final addendum — read once, then stop collecting frameworks)

Adds two things from external research to `blueprint.md`. This is the
last planned addition to the toolkit — further research into ADR/
documentation frameworks has diminishing returns at solo-dev scale and
becomes its own procrastination loop.

---

## Addition 1 — Three separate dimensions (extends Step 1 of blueprint.md)

Every piece of content has three independent properties. Don't conflate
them, and don't build folders by the middle one:

1. **Type** — what kind of knowledge it is (decision, reference,
   architecture, research...). This is what Step 1/2/3 of the blueprint
   already sorts by. This is what determines the folder.
2. **Format/methodology** — how it's written (Nygard vs MADR vs arc42 vs
   plain notes). This is a detail of the template used *within* a type —
   never a folder name.
3. **Lifecycle stage** — ephemeral → evidence-producing (temporary) →
   current/active → historical (superseded). This determines status
   field and whether it's worth keeping at all, not where it lives.

## Addition 2 — Full ADR status lifecycle (replaces the simple
Accepted/Superseded in blueprint.md Step 5)

```
Proposed → Under Review → Accepted → Implemented
                                          │
                          ┌───────────────┴───────────────┐
                          ▼                                ▼
                     Superseded                     Rejected / Deprecated
                    (by new ADR)
```

Use `Proposed` while you're still weighing it in the same session,
`Accepted` once committed (this is the status nearly all of yours will
carry, since you write ADRs after deciding, not before). `Rejected` is
for an alternative you seriously considered and wrote up, then didn't
choose — rare for solo work, skip unless it happens naturally.

---

## Explicitly deferred (do not build now)

- Traceability matrix (Requirement → ADR → Design → PoC → Test)
- Dedicated Archive/ folder (status field + your existing index already
  gives you this)
- Risk register, changelog, formal requirements docs as separate folders
- Any Governance/Compliance layer (Architecture Review Records,
  Compliance Evidence, Traceability Matrix Governance) — this is for
  organizations under external audit, not solo projects

Revisit only if/when you have a genuine backlog of tracked risks, a
public changelog audience, or compliance pressure — not preemptively.

---

**Next step is not another framework.** Take one real planning
conversation and run `adr-extraction-prompt.md` on it. The toolkit is
complete; the bottleneck now is using it, not refining it further.

--- FILE: blueprint.md ---

# Documentation & Decision Blueprint (Master — v1)

Paste this whole file into any AI conversation and ask: "Using this
blueprint, classify this conversation's content and tell me where each
piece goes." Works for any project type — SaaS, GaaS, AI platform/hosting,
Android/iOS, AI services, anything.

---

## Step 0 — Does this even deserve a record?

Run this BEFORE anything else. For a candidate decision, ask:

- High business value or risk impact?
- A key stakeholder's concern (even if that's just future-you)?
- A new/advanced quality requirement (perf, security, offline capability)?
- An external dependency challenge (licensing, vendor, platform limit)?
- Cross-cutting, system-wide impact?
- First of its kind in this codebase?
- An area that's been troublesome before?

**None apply → don't write an ADR.** Either drop it, or it belongs in an
architecture doc / reference note instead (Step 1 below).

**Concrete non-examples** (never ADRs, no matter how long they were
discussed): installing a package, running one test, tweaking a config
value (e.g. "changed temperature 0.7→0.3"), trying one prompt, or
downloading/testing a model without a comparison being settled. These
are experiment/config history — log them as a line in a benchmark or
experiment note if useful, never as an ADR.

For candidate reference/architecture/roadmap content, there's no gate —
if it's genuinely reusable knowledge or describes the system, it's worth
keeping; just route it correctly with Step 1.

---

## Step 1 — Classify the content type

A single conversation usually contains MULTIPLE types. Split it — don't
force everything into one document.

| # | Type | Test question | Format |
|---|------|---------------|--------|
| 1 | **Decision (ADR)** | Did we choose between real alternatives and commit? | ADR template (Step 5) |
| 2 | **Reference / Methodology** | Reusable know-how, comparison, or glossary — not tied to one choice? | Freeform doc |
| 3 | **Architecture (current-state)** | Describes how the system IS, not why? | architecture.md |
| 4 | **Roadmap / Vision** | About future direction or priorities? | roadmap.md / vision.md |
| 5 | **Benchmark log** | Raw test data plus why it was tested? | benchmark-results/*.md |
| 6 | **Runbook / Procedure** | Step-by-step instructions for when X happens? | runbook.md |
| 7 | **Diagram** | Best expressed visually? | .drawio / .svg |

**Rule of thumb:** if you're tempted to write "why we picked X" AND
"general knowledge about X-type things" in the same file, that's two
files — an ADR (type 1) that *links to* a reference doc (type 2).

---

## Step 2 — Scope test (three tiers)

1. Affects more than one project, OR about shared infra/hardware/model
   weights themselves? → **Platform** → `KnowledgeBase/`
2. Affects some but not all projects within one domain (e.g. all Android
   apps, but not a backend service)? → **Shared** → `AndroidLab/Shared/`
   (or equivalent domain-shared folder)
3. Otherwise → **Project** → that project's own numbered folder

---

## Step 3 — File location by type × scope

| Type | Platform | Shared | Project |
|---|---|---|---|
| Decision (ADR) | `05_Decisions/` | `ADR_Templates/` or domain subfolder | `08_ADRs/` |
| Reference/Methodology | `08_References/` | domain folder (e.g. `Mobile_AI/`) | `11_References/` |
| Architecture | `02_AI_Infrastructure/` | `Android_Architecture/` | `02_Architecture/` |
| Roadmap/Vision | rare at platform level | — | `01_Product/`, `10_Roadmap/` |
| Benchmark log | `04_Projects/<ModelCore>/benchmark-results/` | — | `07_Research/benchmark-results/` |
| Runbook | `06_Runbooks/` | — | `09_Runbooks/` |
| Diagram | `07_Diagrams/` | — | project's architecture folder |

**Create folders lazily.** Don't pre-build every folder in Step 3/4 up
front — only create a folder the first time you actually have content
for it. An empty scaffold recreates the same over-organizing problem at
the filesystem level.

---

## Step 4 — Universal project template

Clone for every new project, any domain (create folders as needed, not
all at once — see the lazy-creation note above):

```
<ProjectName>/
├── 01_Product/        vision, problem statement, target users
├── 02_Architecture/   current-state design (the "how it is")
├── 03_UX/             interface design (or API_Design for backend/SaaS)
├── 04_Core_System/    domain logic (rename per project)
├── 05_Security/
├── 06_Performance/
├── 07_Research/        methodology notes, POC logs, benchmark-results/
├── 08_ADRs/            project-scoped decisions only
├── 09_Runbooks/
├── 10_Roadmap/
└── 11_References/      external links, glossaries, format comparisons
```

---

## Step 5 — ADR format

Default: **Nygard-lite**, plus a source pointer so the origin is never
lost without needing to keep the full transcript.

```
# ADR-XXXX: <short title>
Date: <date>
Status: Accepted
Source: <conversation date/name this came from>
## Context
<1-3 sentences: what prompted this>
## Decision
<1-3 sentences: what was decided>
## Consequences
<bullets: good and bad — every ADR needs at least one real downside>
## Alternatives Considered
<bullets: only options you genuinely weighed>
```

Add MADR-style per-option pros/cons only when you seriously weighed 3+
options and want that preserved. Skip TOGAF, Tyree & Akerman (IEEE), AWS
Perspective, and CR→RFC→ADR workflows — all built for large teams
coordinating review across many people; for solo work, CR/RFC content
just becomes the ADR's own Context/Alternatives sections.

**Not yet ready for a full ADR?** Log it as `Pending` in the relevant
`ADR-INDEX.md` (Status column) instead of writing the full record. Only
promote it to a numbered ADR once it's actually settled.

---

## Step 6 — Timing: Most Responsible Moment (MRM)

Decide costly-to-reverse things (core runtime, storage engine, embedding
approach) **early**, once the problem is understood — not at the last
possible moment in the name of flexibility.
- Too early → locked in before you had enough information
- Too late → months built on the wrong assumption

**Before writing:** stakeholders known? Timing right (not too early/late)?
2+ real alternatives? Driving requirement clear? Template picked?

**After writing:** reasoning (not just verdict) written down? You still
agree with it on re-read? Filed in the right place? Changed later → new
ADR marked "supersedes," never edit an Accepted one.

---

## Step 7 — Anti-patterns (avoid these — they're what caused the original mess)

- **Mega-ADR / Novel-Epic** — a whole architecture discussion or design
  doc squeezed into one record. Fix: split by type (Step 1) first.
- **Fairy Tale** — only pros listed, no real cons.
- **Free Lunch Coupon** — consequences section lists only harmless ones.
- **Dummy Alternative** — a fake option listed just to make the real
  choice look considered.

---

## Step 8 — Reading old records after a gap

Never read files one by one. Read the index (one line per record, see
`ADR-INDEX-template.md`), open only what's relevant to today's task. The
Status column doubles as your lightweight decision log — `Pending`,
`Accepted`, or `Superseded by ADR-XXXX` — no separate decision-log file
needed.

--- FILE: documentation_maturity_landscape.md ---

# Documentation Maturity Landscape (reference only — not a roadmap)

This is orientation knowledge: it explains where different documentation
practices sit in the industry, so you recognize a term or format when
you encounter it. **It is not a checklist to progress through.** Nothing
in Staff/Principal or Architect/Enterprise rows applies to a solo
project — those describe organizational coordination problems (cross-
team proposals, governance, portfolio management) that don't exist
without a team or portfolio to coordinate. Don't reach for them.

Your actual working level is Mid, with one item borrowed from Senior
(MADR-style ADRs, already folded into `blueprint.md`). That's enough.

## Taxonomy
```
ADR            → MADR
Architecture   → arc42 + C4
Proposal       → RFC
Requirements   → SRS/PRD
Implementation → HLD/LLD
Operations     → Runbook
History        → Changelog
Traceability   → REQ → ADR → DESIGN → TEST
```

## Why these artifacts exist and how they interact
```
Business / Product
       ↓
Requirements
       ↓
Unknown / Question
       ↓
Research / Spike / PoC
       ↓
Proposal / RFC
       ↓
Architecture discussion
       ↓
ADR
       ↓
Architecture
       ↓
Detailed Design
       ↓
Implementation
       ↓
Tests
       ↓
Operations
       ↓
Change
       ↓
New ADR
```

## Traceability concept
```
REQ-023 → ADR-014 → DESIGN-007 → PoC-012 → Implementation → TEST-031
```
(Deferred at your current scale — see `blueprint-integration-final.md`.)

## Practice by experience level

**Junior**
README, API documentation, basic design document, meeting notes

**Mid-level** ← you are here
HLD, LLD, SRS/PRD, API contracts, basic ADR, runbooks

**Senior**
MADR, RFC, arc42, C4, research/PoC, risk/debt tracking, operational
documentation, ADR lifecycle

**Staff / Principal** (not applicable solo)
documentation lifecycle, traceability, decision history, architecture
evolution, governance, cross-team proposals, requirements → architecture
→ implementation → verification chains

**Architect / Enterprise Architect** (not applicable solo)
all of the above, plus TOGAF/architecture governance, stakeholder
concerns, architecture viewpoints, business/data/application/technology
architecture, compliance, portfolio governance, organizational
architecture

