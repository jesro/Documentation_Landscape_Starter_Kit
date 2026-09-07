# The Full Documentation Landscape for Software/Architecture Work

Your original list (Nygard, MADR, Tyree & Akerman, Y-Statements, AWS Perspective, TOGAF) is
**only one slice** of the landscape — single-decision ADR formats, plus one whole-system
framework (TOGAF). The real question you're asking spans the entire lifecycle of how a system's
knowledge gets captured: why decisions were made, what the system is, how it's built, how it's
run, and how all of that evolved over time.

Below: (1) a comprehensive *practical* landscape of the major documentation artifact types and
established methodologies — not an exhaustive list, since organizations invent their own
variants and there's no finite authoritative catalog — (2) what/when/why for each, and
(3) how to think about lifespan and lifecycle, which is the part most lists skip.

**Three dimensions that get conflated but shouldn't be:**

1. **Artifact type** — ADR, RFC, HLD, LLD, PoC report, runbook, etc. (*what* it is)
2. **Methodology/framework** — MADR, arc42, TOGAF, C4, 4+1, Rozanski & Woods, etc. (*how* it's structured)
3. **Lifecycle stage** — ephemeral → temporary/evidence-producing → current → historical (*how long it lives*)

A given piece of knowledge has all three: e.g. an ADR (type) written in MADR format (methodology)
that is currently active (lifecycle stage). Keep these separate when organizing — don't build
folders by methodology, build them by *what kind of knowledge it is*, and let the methodology be
a detail of how each entry is written.

---

## 1. Decision Records (single decision, "why")

| Format | What it is | When to use | Why |
|---|---|---|---|
| **Nygard ADR** | 5 fields: Title, Status, Context, Decision, Consequences | Default for small teams / first ADRs | 10-minute write, zero training needed |
| **MADR** | Adds Decision Drivers, Considered Options, Pros/Cons | You need to show alternatives were seriously evaluated | Modern default; has tooling (VS Code, adr-tools) |
| **Tyree & Akerman (IEEE 2005)** | Heavyweight: Issue, Positions, Argument, Implications, links to requirements/principles | Regulated industries needing full audit trails | Nothing gets lost; traceable to compliance requirements |
| **Y-Statements** | One compressed sentence: "In context X, facing Y, we chose Z to achieve Q, accepting W" | Workshops, katas, rapid-fire decision capture | You can log 15 in a session; expand important ones later |
| **AWS Perspective ADR** | Nygard-like, cross-referenced to Well-Architected pillars | Cloud migrations, AWS shops | Plays well with other AWS artifacts |
| **RFC-style** (Rust RFCs, K8s KEPs, IETF RFCs) | Summary, Motivation, Detailed Design, Drawbacks, Alternatives, Unresolved Questions | Decision affects many teams, needs open consensus | Review process is built into the artifact itself |
| **Alexandrian/Pattern-form** | Title, Prologue, Problem, Forces, Solution, Consequences | Decision is really a reusable pattern | Forces you to name competing pressures explicitly |
| **Joel Parker Henderson collection** | Not a format — a GitHub repo bundling all the above | Picking a starting template | Saves you from bikeshedding |

## 2. Proposal / Review Documents (before a decision is made)

| Format | What it is | When to use |
|---|---|---|
| **RFC / design proposal** | Pre-decision write-up for feedback | Cross-team impact, need buy-in before committing |
| **KEP (Kubernetes Enhancement Proposal)-style** | Structured proposal + review workflow | Platform/open-source feature proposals |

## 3. Whole-System Architecture Description

| Format | What it is | When to use | Why |
|---|---|---|---|
| **arc42** | 12-section free template (Context, Solution Strategy, Building Blocks, Runtime, Deployment, Crosscutting Concepts, **has a built-in ADR section**, Risks) | Structured whole-system docs without enterprise bureaucracy | Lightweight, pragmatic, ADRs slot right in |
| **TOGAF ADM** | Full Architecture Definition Document across Business/Data/App/Tech layers, formal governance gates | Large enterprise already running TOGAF | Gives architecture a seat in portfolio/budget governance |
| **ISO/IEC/IEEE 42010** | Not a template — the standard defining what "architecture description" *means* (stakeholders, concerns, viewpoints) | You need standards-compliance (gov contracts, certifications) | Most other frameworks are built to conform to it |

## 4. Architecture Views / Diagrams (accompany #3, not a replacement)

| Format | What it is | When to use |
|---|---|---|
| **C4 Model** | Context → Container → Component → Code, four zoom levels | Almost always — pairs with arc42/ADRs to standardize diagrams |
| **4+1 View Model** | Logical, Process, Development, Physical views + Scenarios | Legacy RUP shops, academic/certification contexts |
| **Rozanski & Woods Viewpoints & Perspectives** | Viewpoints (Functional, Information, Concurrency...) crossed with Perspectives (Security, Performance, Availability...) | Complex distributed systems where cross-cutting quality attributes need explicit treatment |

## 5. Requirements Documentation ("what it must do")

- **SRS (Software Requirements Specification)** — formal functional/non-functional spec
- **PRD (Product Requirements Doc)** — product-facing requirements, less formal than SRS
- **Use cases / user stories** — scenario-based requirements
- **Quality-attribute scenarios** — testable statements of a quality goal (e.g. "99.9% availability under 10x load")

Use when: before or alongside design, to anchor decisions to actual needs; especially valuable for traceability (Tyree & Akerman, TOGAF, 42010 all reference back to this layer).

## 6. Design Documentation ("how a piece works")

- **HLD (High-Level Design)** — component boundaries, data flow, integration points
- **LLD (Low-Level Design)** — class/function-level detail, algorithms, schemas
- **API specs / contracts** (OpenAPI, protobuf) — interface documentation
- **Data models / data dictionaries** — schema and semantics of stored data

Use when: implementing a specific feature or component; these are more granular and shorter-lived than #3.

## 7. Research / Exploration ("we didn't know, so we investigated")

- **Spike** — timeboxed investigation to reduce uncertainty
- **PoC (Proof of Concept)** — working code proving feasibility, not production-ready
- **Feasibility study** — broader viability assessment (cost, risk, technical)
- **Benchmark report** — comparative performance data

Use when: genuine unknowns exist before a decision can be made responsibly. These often *feed into* an ADR but aren't ADRs themselves.

## 8. Risk & Debt Documentation

- **Risk register / architecture risk assessment** — tracked risks with likelihood/impact/mitigation
- **Technical debt log** — known shortcuts and their cost of not fixing
- **Threat model / security architecture doc** — attack surface, mitigations

Use when: continuously, as a living document — not a one-time artifact.

## 9. Change / History Records

- **Changelog** — what changed, per release
- **Decision log** — a flat, dated ledger of decisions (often lighter-weight than a full ADR set, or an index *into* your ADRs)
- **Migration record / deprecation notice** — what was replaced, when, why

## 10. Conversation / Meeting Records

- **Meeting notes / architecture workshop notes** — raw discussion capture
- **Design discussion threads** — the "conversation" layer that precedes a decision

**Important distinction:** most conversations should *stay* conversations. Only promote one to an ADR when it becomes a real architectural commitment — not every discussion deserves a formal decision record.

## 11. Operational Documentation

- **Runbooks / playbooks** — step-by-step operational procedures
- **Deployment docs** — how to ship/release
- **Incident reports / postmortems** — what broke, why, what changed as a result

## 12. Knowledge / Reference Documentation

- **Developer docs, API docs, glossaries, coding conventions** — stable, low-churn reference material

## 13. Governance / Compliance

- **Architecture review records, traceability matrices, compliance evidence** — demonstrate that governance actually happened (mainly relevant if you're under TOGAF/42010/regulated-industry pressure)

## 14. Project / Product Documentation

- **PRD, roadmap, project charter, release plan** — the "why are we building this at all" layer, sits above architecture

---

## The lifespan dimension (this is the part your original list misses)

Documentation isn't just categorized by *type* — it's categorized by how long it should live and what happens to it after it's superseded.

| Lifespan | Examples | What happens to it |
|---|---|---|
| **Ephemeral** | Raw conversation, brainstorm, scratch notes | Useful during exploration; may be discarded once the useful part is extracted |
| **Temporary but evidence-producing** | Spike, PoC, benchmark, feasibility study | Answers "we didn't know X, so we checked" — may be archived once findings are incorporated elsewhere |
| **Long-lived / current** | Architecture doc, requirements, design, ADR (active), API contract | Should survive personnel turnover and iteration; kept up to date |
| **Historical** | Superseded ADR, old architecture version, incident report, changelog entry | No longer describes the current system, but should **not be deleted** — it explains how you got here |

A useful rule of thumb:

> **Current documentation describes what is true now.**
> **Decision documentation explains why it became true.**
> **Historical documentation explains what used to be true, and how it changed.**

### The ADR has its own lifecycle

```
PROPOSED → UNDER REVIEW → ACCEPTED → IMPLEMENTED
                                          │
                          ┌───────────────┴───────────────┐
                          ▼                                ▼
                     SUPERSEDED                    REJECTED / DEPRECATED
                    (by new ADR)
```

Don't delete `ADR-003: Use SQLite` when you later write `ADR-019: Replace SQLite with
PostgreSQL`. Instead, mark ADR-003's status as "Superseded by ADR-019." The chain is the value.

### How conversation becomes documentation

```
Conversation → Question/Problem → Research/Spike/PoC → Options weighed →
Design discussion → Decision → ADR → Implementation → Architecture/code/runbook →
(later) Change → New ADR
```

Not every step needs a permanent artifact. Most conversations and spikes stay ephemeral;
only the load-bearing decisions get promoted into ADRs.

---

## Practical recommendation

- **Individual decisions:** MADR (default) → Tyree & Akerman only if compliance genuinely
  requires the audit trail → Y-Statements for fast workshop capture that you later expand.
- **Whole-system description:** arc42 (has an ADR slot built in) unless you're already locked
  into TOGAF governance.
- **Diagrams:** C4, paired with whichever of the above you're using — not a standalone choice.
- **Everything else** (requirements, design docs, risk register, runbooks, changelog,
  meeting notes) — organize by the *kind of knowledge*, not by which template family it came
  from.

### Suggested folder structure (organize by information, not by methodology)

```
KnowledgeBase/
├── 01_Context/            vision, goals, stakeholders, constraints
├── 02_Requirements/       functional, quality-attributes, use-cases
├── 03_Architecture/       overview, context, containers, components, deployment (arc42-style)
├── 04_Decisions/          ADR-001, ADR-002, ... (MADR format, with status/superseded tracking)
├── 05_Design/             HLD, LLD, API specs, component design
├── 06_Research/           spikes, PoCs, benchmarks, feasibility studies
├── 07_Risks/              risk register, technical debt log, threat models
├── 08_Operations/         runbooks, deployment docs, incident reports
├── 09_Changes/            changelog, migration records, deprecations
├── 10_Conversations/      workshop notes, design discussions, meeting notes
├── 11_References/         external docs, standards, links
├── 12_Glossary/
├── 13_Traceability/       requirement ↔ decision ↔ design ↔ implementation ↔ test links
└── 14_Archive/            superseded ADRs, old architecture versions, retired docs
```

Each artifact picks its own template based on which folder it lives in — a decision in
`04_Decisions/` is MADR, a system overview in `03_Architecture/` follows arc42, a discussion in
`10_Conversations/` is just notes. The same project can and should use several formats
simultaneously; the folder (i.e., the *kind of knowledge*) determines the template, not the
other way around.

**Why `13_Traceability/` matters once a project grows:** a folder of Markdown files alone can't
answer "what requirement led to this decision, and what tests verify it's still satisfied?"
Traceability is the explicit chain that connects them, e.g.:

```
REQ-023 "AI inference must work without network access"
   → ADR-014 "Use local inference rather than cloud API"
      → DESIGN-007 "Model execution architecture"
         → PoC-012 "Benchmark llama.cpp vs alternative X"
            → Implementation
               → TEST-031 "Offline inference test"
```

**Why `14_Archive/` matters — but only past a certain size:** for a Git-backed KnowledgeBase,
`Status: Superseded` + cross-links + commit history already give you a historical trail without
a separate folder — a superseded ADR can just stay in `04_Decisions/` with its status updated.
A dedicated `Archive/` becomes worth the overhead once the active set is large enough that
historical entries start interfering with day-to-day navigation and search. Treat it as an
**organizational optimization you add later, not a requirement from day one.**

### Don't build every format on day one

A stable core is enough to start; add specialized formats only when a real need (compliance,
scale, governance) demands them:

| Need | Artifact | Recommended starting format |
|---|---|---|
| Capture a discussion | Conversation note | Plain Markdown |
| Investigate an unknown | Research / spike | Plain Markdown |
| Compare technical options before committing | Design proposal | RFC-style |
| Make an architectural commitment | ADR | **MADR** |
| Describe the whole system | Architecture doc | **arc42 + C4** |
| Describe one feature's implementation | Design doc | HLD/LLD |
| Track a known problem | Risk/debt record | Structured Markdown |
| Explain how to operate something | Runbook | Procedure list |
| Record a major change | Migration/change record | Structured Markdown |
| Preserve history | Archived doc | Original artifact, moved as-is |

Reach for Tyree & Akerman, TOGAF, 4+1, or similar heavier frameworks only when their specific
governance, audit-trail, or modeling requirements are actually imposed on you — not by default.
