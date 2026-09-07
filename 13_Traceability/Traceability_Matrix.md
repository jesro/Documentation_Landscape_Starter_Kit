# Traceability Matrix

The goal is to make the knowledge chain explicit:

```text
Requirement
   -> Decision
      -> Design
         -> Research / Evidence
            -> Implementation
               -> Test
```

## Matrix

| Requirement | Decision | Design | Research | Implementation | Test | Status |
|---|---|---|---|---|---|---|
| REQ-023 | ADR-014 | DES-007 | POC-012 | | TEST-031 | |

## Example

```text
REQ-023 "AI inference must work without network access"
   -> ADR-014 "Use local inference rather than cloud API"
      -> DES-007 "Model execution architecture"
         -> POC-012 "Benchmark llama.cpp vs alternative X"
            -> Implementation
               -> TEST-031 "Offline inference test"
```

## Coverage checks

- Requirements without design:
- Requirements without tests:
- Decisions without evidence:
- Design without requirements:
- Risks without mitigation:
