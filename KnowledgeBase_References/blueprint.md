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
