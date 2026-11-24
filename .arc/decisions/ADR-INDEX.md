# ADR Index

One line per decision — the rule, not the reasoning. Read the full ADR (`.arc/decisions/ADR-NNNN-*.md`) for context and rationale.

## Accepted — binding rules

| ADR | Category | Status | Rule |
|---|---|---|---|
| ADR-0001 | component | accepted | Client-side UI code lives in this component and reaches server-side data only through the backend API, never directly. |

## Proposed — not binding (assumptions awaiting a person's confirmation)

| ADR | Category | Status | Rule |
|---|---|---|---|
| ADR-0002 | deployment_target | proposed | Package the Source service as a container image built from its Dockerfile. |
| ADR-0003 | cross_cutting | proposed | Users authenticate to the Source service with JWTs it issues and verifies itself. |
