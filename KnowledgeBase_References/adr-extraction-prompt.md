# ADR Extraction Prompt (run at the end of any planning conversation, same session)

```
Using the Documentation & Decision Blueprint I've shared, go through this
conversation and:

1. Apply Step 0 (the ASR gate) — only proceed with items that pass it.
2. Classify every remaining piece of content by type (Step 1).
3. For anything that is a Decision, output it as a separate ADR using
   the Step 5 template exactly:

# ADR-XXXX: <short title>
Date: <today's date>
Status: Accepted
## Context
<1-3 sentences>
## Decision
<1-3 sentences>
## Consequences
<bullets, at least one real downside>
## Alternatives Considered
<bullets, only genuinely-weighed options>

4. For anything that is Reference/Architecture/Roadmap/Benchmark/Runbook
   content, just label it with its type and a one-line description —
   don't format it as an ADR.
5. For each item, tell me where it should be filed per Step 2/3 (platform,
   shared, or project — and which folder).

Do not summarize the whole conversation. Only extract things that were
actually decided or that constitute real reusable content — not things
merely discussed or left open. Number ADRs starting from <next free
number in your index>.
```
