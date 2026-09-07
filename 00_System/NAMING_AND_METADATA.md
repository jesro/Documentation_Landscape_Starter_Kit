# Naming, IDs and Metadata

## Naming

Use stable IDs where an artifact participates in traceability.

Suggested prefixes:

- CTX-### — Context
- REQ-### — Requirement
- ARC-### — Architecture document
- ADR-### — Architecture decision
- PROP-### — Proposal
- DES-### — Design
- SPIKE-### — Spike
- POC-### — Proof of Concept
- FEAS-### — Feasibility study
- BENCH-### — Benchmark
- RISK-### — Risk
- DEBT-### — Technical debt
- TM-### — Threat model
- CHG-### — Change
- MIG-### — Migration
- DEP-### — Deprecation
- CONV-### — Conversation
- RUN-### — Runbook
- INC-### — Incident
- GOV-### — Governance review
- TEST-### — Test evidence

## Common metadata

```yaml
---
id: ADR-001
title: "..."
type: adr
methodology: madr
status: proposed
lifecycle: current
created: YYYY-MM-DD
updated: YYYY-MM-DD
owners:
  - ...
tags:
  - ...
related:
  requirements: []
  decisions: []
  designs: []
  research: []
  tests: []
supersedes: []
superseded_by: []
---
```

Use only fields that add value. Metadata should support navigation, automation and traceability,
not become bureaucracy.
