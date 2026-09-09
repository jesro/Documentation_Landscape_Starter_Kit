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
