---
id: ADR-0002
category: deployment_target
title: 'Deployment target: Hosting is not chosen yet: run locally or dev-only for
  now'
status: proposed
superseded_by: null
component_id: null
rule: Package the Source service as a container image built from its Dockerfile.
decision: 'Hosting is not chosen yet: run locally or dev-only for now. The Source
  service has a Dockerfile, so it runs as a container; the React client is served
  by its own dev or static server. Cloud provider, region topology and data residency
  are open.'
evidence:
- type: scan
  ref: Dockerfile
- type: human
  ref: recommended default, accepted by the human without review
basis: assumed
---

## Decision

**Rule.** Package the Source service as a container image built from its Dockerfile.

Hosting is not chosen yet: run locally or dev-only for now. The Source service has a Dockerfile, so it runs as a container; the React client is served by its own dev or static server. Cloud provider, region topology and data residency are open.

## Evidence

Basis: assumed.
- scan: Dockerfile
- human: recommended default, accepted by the human without review
