# triage

Classify, extract, route. A service that pulls open issues from a public GitHub
repository, classifies each one, extracts structured fields, scores its own
confidence, routes low-confidence items to a review queue, and posts a digest on
a schedule.

Built as an eight-week learning project — TypeScript, SQL, Python and n8n — with
commits dated as the work happened rather than backfilled.

## Why this design

Three decisions worth stating up front, since they are the ones that carry over
from production document-processing work:

- **Classification and extraction are separate steps.** Classifying first means
  the extraction prompt only has to handle one document shape at a time, which
  makes both the prompt and the failure modes easier to reason about.
- **Confidence gates the automation, not the model.** Anything below the
  threshold goes to a human review queue instead of being written as fact. The
  interesting product question is where the threshold sits, and what it costs to
  move it.
- **Structured output over prose parsing.** The model is asked for a defined
  schema, not for text that then gets regexed. Parsing prose is where these
  pipelines rot.

## Architecture

| Layer | Stack |
|---|---|
| Ingest | TypeScript, GitHub REST API, scheduled pull |
| Classify | Claude API (`@anthropic-ai/sdk`), structured outputs |
| Store | Postgres — raw issue, prediction, confidence, review status |
| Report | SQL — category mix, week-over-week movement, queue depth |
| Evaluate | Python — hand-labelled set, accuracy, prompt comparison |
| Orchestrate | n8n — schedule the run, post the digest, alert on queue depth |

## Status

Week 1 of 8. Setup and n8n.

- [ ] 1 — Setup, n8n workflows
- [ ] 2 — TypeScript foundations, a working CLI
- [ ] 3 — Modules, config, error handling, first test
- [ ] 4 — Claude API, classification, confidence threshold
- [ ] 5 — Postgres, schema, persistence
- [ ] 6 — CTEs and window functions, the digest query
- [ ] 7 — Python eval harness, a real accuracy number
- [ ] 8 — End-to-end orchestration, write-up

## Data

Public GitHub issues only. No proprietary data of any kind enters this
repository.

## Notes

`LEARNED.md` holds one line per working session — what got built, what broke,
what became clear.
