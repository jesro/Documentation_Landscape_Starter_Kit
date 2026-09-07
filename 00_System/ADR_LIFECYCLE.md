# ADR Lifecycle

```text
PROPOSED
   |
   v
UNDER REVIEW
   |
   v
ACCEPTED
   |
   v
IMPLEMENTED
   |
   +-------------------+
   |                   |
   v                   v
SUPERSEDED       REJECTED / DEPRECATED
   |
   v
Successor ADR
```

## Status definitions

### Proposed

A candidate decision exists but is not committed.

### Under Review

Relevant stakeholders are evaluating it.

### Accepted

The organization/project has committed to it.

### Implemented

The decision is reflected in the system.

### Superseded

A later decision replaces it. Keep the original.

### Rejected / Deprecated

The proposal or decision is no longer valid for use.

## Supersession rule

Never erase the historical rationale.

Example:

`ADR-003: Use SQLite`

later becomes:

`ADR-019: Replace SQLite with PostgreSQL`

ADR-003 should say:

`Status: Superseded by ADR-019`
