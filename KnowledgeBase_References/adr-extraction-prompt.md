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
