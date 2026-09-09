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
