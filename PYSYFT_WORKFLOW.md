## PySyft + PPRL Workflow Diagram for CTOT / SLDS Data

```text
┌──────────────────────────────────────────────┐
│  1. Researchers / BrightQuery / CTOT Team    │
│  Request access from State Data Owner        │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  2. State Data Owner Reviews Request         │
│  - Research purpose                          │
│  - Legal / DUA requirements                  │
│  - Privacy and disclosure rules              │
│  - Requested datasets and fields             │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  3. State Provides Approved Metadata         │
│  - Data dictionary                           │
│  - Schema                                    │
│  - ERD                                       │
│  - Code lists                                │
│  - Mock / synthetic data structure           │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  4. Researchers Develop Code                 │
│  Using Synthetic / Mock Data                 │
│                                              │
│  - CTOT analysis code                        │
│  - PPRL linkage logic, if needed             │
│  - Privacy rules                             │
│  - Aggregate output design                   │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  5. PPRL Logic                               │
│  Record Linkage Engine                       │
│                                              │
│  - Generates linkage tokens                  │
│  - Matches education, workforce, wage data   │
│  - Tested only on synthetic data first       │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  6. Submit Code Through PySyft               │
│  PySyft manages request workflow             │
│                                              │
│  - Code submission                           │
│  - Review request                            │
│  - Execution request                         │
│  - Audit trail                               │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  7. State Reviews Submitted Code             │
│                                              │
│  Checks for:                                 │
│  - No raw record output                      │
│  - No identifiers                            │
│  - No small-cell disclosure                  │
│  - Approved fields only                      │
│  - Correct research purpose                  │
└──────────────────────┬───────────────────────┘
                       │
              ┌────────┴────────┐
              ▼                 ▼
┌──────────────────────┐  ┌──────────────────────┐
│  Reject / Revise     │  │  Approve Code         │
│  Researcher updates  │  │  Run on private data  │
│  code and resubmits  │  │  inside state env     │
└──────────┬───────────┘  └──────────┬───────────┘
           │                         │
           └─────────────┬───────────┘
                         ▼
┌──────────────────────────────────────────────┐
│  8. Secure Execution on State Private Data   │
│                                              │
│  Real SLDS data remains with the state       │
│  Researchers do not see raw records          │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  9. State Reviews Output                     │
│                                              │
│  - Aggregate only                            │
│  - Small cells suppressed                    │
│  - No person-level records                   │
│  - No SSN / name / individual wage data      │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  10. Researchers Receive Approved Outputs    │
│                                              │
│  Examples:                                   │
│  - Transition counts                         │
│  - Wage growth                               │
│  - Employment retention                      │
│  - CTOT pathway validation metrics           │
│  - Linkage-quality summaries                 │
└──────────────────────────────────────────────┘
```

## Simple version

```text
BrightQuery / CTOT
        │
        │ request access
        ▼
State Data Owner
        │
        │ provides metadata + mock data
        ▼
Researchers develop CTOT + PPRL code
        │
        │ submit code
        ▼
PySyft
        │
        │ manages review + secure execution
        ▼
State reviews and approves code
        │
        │ runs on private SLDS data
        ▼
State reviews output
        │
        │ releases safe results only
        ▼
BrightQuery receives approved aggregate outputs
```

## Key message

```text
PPRL = Record linkage engine
PySyft = Secure execution and governance platform
State = Owner of private SLDS data
BrightQuery / CTOT = Researcher receiving only approved outputs
```

## PySyft methodology

| Step | Stage | Lead | Methodology |
| --- | --- | --- | --- |
| 1 | Intake request | Researcher | Submit research purpose, dataset scope, fields, linkage goal, and requested outputs. |
| 2 | Metadata approval | State owner | Approve schema, data dictionary, ERD, mock-data structure, and disclosure rules. |
| 3 | Mock-data development | Researcher | Build and test PPRL and analytics code without seeing real private records. |
| 4 | Code submission | Researcher | Submit versioned code, thresholds, dependencies, privacy controls, and test evidence. |
| 5 | Owner review | State owner | Check purpose fit, identifier handling, PPRL risk, output schema, and disclosure controls. |
| 6 | Governed execution | PySyft / state environment | Run approved code near private data with raw records inaccessible to researchers. |
| 7 | Output review | State owner | Review aggregate tables, linked IDs, match scores, small cells, and re-identification risk. |
| 8 | Approved release | PySyft / state environment | Release only approved outputs and preserve the request, review, execution, and release audit trail. |

Required artifacts:

- request record and owner decision
- approved metadata and mock-data validation evidence
- versioned PPRL and analytics code package
- output schema and disclosure-control plan
- PySyft audit trail for submission, review, execution, and release

## Related Local Document

- `LINKAGE_TOOL_FLOW_PYSYFT_PPRL.md`




