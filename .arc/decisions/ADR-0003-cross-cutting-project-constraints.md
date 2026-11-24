---
id: ADR-0003
category: cross_cutting
title: 'Cross-cutting: Project constraints'
status: proposed
superseded_by: null
component_id: null
rule: Users authenticate to the Source service with JWTs it issues and verifies itself.
decision: 'Authentication is built into the Source service: it issues and verifies
  JWTs itself (no external identity provider).

  No backlog items belong to this project; components serve no epics.

  No third-party integrations.

  No scale, availability or compliance requirements stated; none are assumed beyond
  a development-grade setup.'
evidence:
- type: scan
  ref: src/app/routes/auth/token.utils.ts
- type: human
  ref: recommended default, accepted by the human without review
basis: assumed
---

## Decision

**Rule.** Users authenticate to the Source service with JWTs it issues and verifies itself.

Authentication is built into the Source service: it issues and verifies JWTs itself (no external identity provider).
No backlog items belong to this project; components serve no epics.
No third-party integrations.
No scale, availability or compliance requirements stated; none are assumed beyond a development-grade setup.

## Evidence

Basis: assumed.
- scan: src/app/routes/auth/token.utils.ts
- human: recommended default, accepted by the human without review
