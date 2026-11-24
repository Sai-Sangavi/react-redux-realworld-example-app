---
id: ADR-0001
category: component
title: React Redux Realworld Example App
status: accepted
superseded_by: null
component_id: comp_react_redux_realworld_example_app
responsibility: Browser single-page app built on React and Redux (entry src/index.js,
  page public/index.html); calls the backend REST API with superagent.
kind: web_ui
split_reason: 'Already built: the React/Redux client at the root of the frontend repository,
  with its own browser runtime, separate from the Express service in the backend repository.'
talks_to:
- component_id: comp_source
  interaction: sync
  evidence: src/agent.js
rule: Client-side UI code lives in this component and reaches server-side data only
  through the backend API, never directly.
evidence:
- type: scan
  ref: src/index.js
- type: scan
  ref: public/index.html
basis: derived
---

## Context

The draft recorded none for this component.

## Decision

**Rule.** Client-side UI code lives in this component and reaches server-side data only through the backend API, never directly.

Browser single-page app built on React and Redux (entry src/index.js, page public/index.html); calls the backend REST API with superagent.

Kept separate because Already built: the React/Redux client at the root of the frontend repository, with its own browser runtime, separate from the Express service in the backend repository..

## Talks to

- **Source** (sync) — src/agent.js

## Alternatives considered

The draft recorded none for this component.

## Consequences

The draft recorded none for this component.

## Evidence

Basis: derived.
- scan: src/index.js
- scan: public/index.html
