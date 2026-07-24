# loc-public-domain-engine

> Rights-gate + polite API protocol over the Library of Congress, fanning cleared public-domain items into transcription/OCR/alt-text/translation/dataset work.  ·  **Risk tier:** med  ·  **Status:** planning

The Library of Congress holds millions of digitized items, a large share of them public domain, and exposes them through a JSON API (`?fo=json`), specialized APIs (Chronicling America historic newspapers), and bulk data offerings. But two hard problems sit between that material and useful public good:

**Definition of shipped:** A cleared, provenance-tracked item pool + contributions accepted upstream (By the People / Commons).

This is a **Hee-Lee Oss** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Get started: https://github.com/Hee-Lee-Oss-Projects/hee-lee-oss-downloads

## Plan
- [PLAN.md](./PLAN.md) — robust enterprise plan (vision, architecture, roadmap, risks; includes an applied-improvements appendix + review sign-off)
- [TASKS.md](./TASKS.md) — schema-mapped task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
hee-lee-oss browse
hee-lee-oss next --repo Hee-Lee-Oss-Projects/loc-public-domain-engine --no-fork
```

## Licensing & review
- Code MIT; outputs CC0/CC-BY per source.
- Risk tier **med** — deeds are *delivered, not merged*; a domain reviewer (and expert sign-off for any high-stakes content) must approve before merge.

> Planning stage; no adopting partner secured yet (`verifiedNeed: false` on delivery-dependent tasks).
