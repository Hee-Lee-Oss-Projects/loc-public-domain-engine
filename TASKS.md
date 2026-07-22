# TASKS — loc-public-domain-engine

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Itemized backlog for the LoC rights-gate + polite API protocol that fans cleared public-domain items
into downstream good-deed tasks. See [`PLAN.md`](./PLAN.md) for context, the rights gate, the polite
protocol, and the roadmap (M0–M3).

## How these tasks map to Hee-Lee Oss

Each task below becomes a Hee-Lee Oss **Task JSON** validated against `packages/schema/src/schemas.ts`.
Field mapping:

- **id** — stable `loc-public-domain-engine-<area>-NNN` (the table ID).
- **title** — the table Title.
- **project** — `loc-public-domain-engine`.
- **type** — one of `code | research | writing | data | design-spec | maintenance` (table "Type").
- **lane** — `donated` for all tasks here (the project lane; the CLI never runs headless). Any future
  metered OCR/translation run would be `funded` and must add `fundedBudgetUsd` (a per-task cap).
- **priority** — `high | medium | low`.
- **domain** — e.g. `["open-culture","public-data","digital-libraries","accessibility","public-domain"]`.
- **riskTier** — `low | medium | high`. Rights/cultural-screen tasks are **medium** (the primary
  gate); scaffolding/docs are **low**. Any downstream task touching high-stakes content inherits that
  lane's **high** tier + expert review.
- **urgent** — boolean (default `false`).
- **deliverable** — `pr | dataset | document | translation` (table "Deliverable").
- **tokenEstimate** — `small | medium | large` (table "Size").
- **status** — `open | in-progress | review | delivered | done` (start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — `jdev1977` / beneficiary class until a named partner/steward is secured.
- **verifiedNeed** — **`false`** while no committed external partner/steward is secured (honest; the
  *gap* is real and internal Hee-Lee Oss consumers are named, but the last-mile beneficiary is TO BE SECURED).
- **outputLicense** — `MIT` (code), `CC0-1.0` (engine metadata: manifests, contract, vocabulary,
  ledger, docs). Downstream derivatives carry their own project's license.

> **Standing guardrail on every task:** (1) **No item is fanned out without an `eligible` rights
> determination from the approved ruleset** — deny by default; ambiguity is quarantined. (2) **No LoC
> access may breach LoC's published rate-limit/crawl policy.** Any task proposing to heuristically
> clear ambiguous items, crawl past LoC's limits, ingest restricted material, or surface living-person
> data is **refused and flagged** — out of scope, full stop.

---

## Milestone M0 — Rights-gate + polite API protocol spine

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| loc-public-domain-engine-rights-001 | Rights-vocabulary mapping + eligibility allow-list (deny-by-default) | design-spec | medium | medium | document | — | Rights reviewer + counsel |
| loc-public-domain-engine-policy-001 | Capture LoC published rate limits + bulk/sitemap offerings into `loc-policy.yml` | research | small | medium | document | — | Politeness/infra owner |
| loc-public-domain-engine-client-001 | Polite LoC client: throttle, conditional requests + cache, backoff/jitter, circuit breaker, contact UA | code | large | medium | pr | loc-public-domain-engine-policy-001 | Politeness/infra owner |
| loc-public-domain-engine-prov-001 | Provenance-manifest format (snapshot + rule + hash + TTL + jurisdiction) | design-spec | small | low | document | loc-public-domain-engine-rights-001 | Maintainer |
| loc-public-domain-engine-screen-001 | Cultural-sensitivity / privacy screen spec (TK Labels, sensitive, living-person) | design-spec | small | medium | document | — | Cultural/privacy reviewer |
| loc-public-domain-engine-ci-001 | CI gates: provenance-completeness linter + rights-gate golden-test corpus | code | medium | low | pr | loc-public-domain-engine-rights-001, loc-public-domain-engine-prov-001 | Maintainer |
| loc-public-domain-engine-partner-001 | LoC Labs / "By the People" outreach + name rights reviewer & counsel | research | small | low | document | — | Maintainer |

**Acceptance criteria (key M0 tasks)**

- **loc-public-domain-engine-rights-001**
  - `rights/vocabulary.yml` maps each LoC / rightsstatements.org / Creative Commons rights value to
    `eligible | ineligible | needs-review` with a recorded rationale.
  - **Deny by default:** any value not affirmatively listed as `eligible` resolves to `ineligible`;
    borderline values resolve to `needs-review` (human adjudication).
  - Pre-1929-by-date eligibility is permitted **only** with an affirmative, unambiguous publication
    date in the item's own metadata; date inference to fill a gap is forbidden.
  - Records the **jurisdiction** of each determination (default U.S.) and the rule that produced it.
  - The ruleset is **counsel/qualified-rights-reviewer signed off** before any use.
- **loc-public-domain-engine-policy-001**
  - `loc-policy.yml` records LoC's **currently published** per-endpoint rate limits, verified and
    **dated**, with the source URL.
  - Available **bulk data / sitemap** offerings are catalogued and marked preferred over per-item
    crawling.
  - The required **contact User-Agent** string (project URL + email) is defined.
- **loc-public-domain-engine-client-001**
  - Enforces `loc-policy.yml` limits via a token-bucket throttle + single-flight concurrency cap.
  - Sends `If-None-Match`/`If-Modified-Since`; caches with ETag/Last-Modified; re-fetches return `304`.
  - Honors `Retry-After`; exponential backoff with jitter on `429`/`5xx`; a **circuit breaker
    auto-pauses + alerts** on sustained errors.
  - Sets the descriptive contact `User-Agent`; writes no secrets to logs/receipts; never runs headless.
- **loc-public-domain-engine-ci-001**
  - CI **fails** on any fanned-out item lacking a complete provenance manifest.
  - A **golden-test corpus** of known items per rights category runs in CI, including **negative cases
    that must be quarantined** (a wrongly-cleared negative case fails the build).
  - CI rejects any item whose rights value is not resolved by the approved vocabulary.

**M0 Definition of Done:** rights-vocabulary allow-list defined and **counsel-signed-off**; polite
client implemented against a dated `loc-policy.yml` (throttle + cache + backoff + circuit breaker +
contact UA); provenance-manifest format defined; cultural-sensitivity screen specified; CI provenance
+ rights-gate golden tests live; LoC Labs outreach started; **a qualified rights reviewer named (hard
exit; if the seat is empty M0 cannot exit — escalate per the documented fallback in PLAN.md)**.
`pnpm build && pnpm test && pnpm lint` green.

---

## Milestone M1 — First cleared corpus + transparency

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| loc-public-domain-engine-data-001 | Run an approved high-PD source (e.g. Chronicling America) through the gate → cleared corpus + manifests | data | large | medium | dataset | loc-public-domain-engine-client-001, loc-public-domain-engine-ci-001 | Rights reviewer |
| loc-public-domain-engine-audit-001 | Stratified rights audit of the M1 corpus (zero confirmed wrong-clears) | research | small | medium | document | loc-public-domain-engine-data-001 | Rights reviewer (independent) |
| loc-public-domain-engine-ledger-001 | Publish the quarantine ledger with reason counts | data | small | low | dataset | loc-public-domain-engine-data-001 | Maintainer |
| loc-public-domain-engine-screen-002 | Run cultural-sensitivity / privacy screen over the corpus; hold flagged items | research | small | medium | document | loc-public-domain-engine-data-001, loc-public-domain-engine-screen-001 | Cultural/privacy reviewer |
| loc-public-domain-engine-partner-002 | Identify & engage ≥1 candidate downstream consumer/steward | research | small | low | document | loc-public-domain-engine-partner-001 | Maintainer |

**Acceptance criteria (key M1 tasks)**

- **loc-public-domain-engine-data-001**
  - One approved high-PD source is run discovery → polite fetch → rights-gate → manifest end-to-end.
  - **100%** of cleared items carry a complete frozen manifest (snapshot + rule + URL + timestamp +
    content hash + TTL + jurisdiction); items without one are not in the cleared set.
  - All access stayed within `loc-policy.yml` limits (no policy breach; cache used for re-fetches).
  - Every `ineligible`/`needs-review` item is recorded in the quarantine ledger with a reason.
- **loc-public-domain-engine-audit-001**
  - A **stratified** sample (≥200 cleared items or whole release; strata by rights category + source
    collection) is independently re-reviewed; **zero confirmed wrong-clears**.
  - The **auditor is independent of the gate run** that produced the clears (no self-grading).
  - Any wrong-clear found triggers a vocabulary/golden-test fix and a re-audit before sign-off.
- **loc-public-domain-engine-ledger-001**
  - The quarantine ledger publishes counts by exclusion reason (restricted, undetermined, needs-review,
    sensitive-hold) so the gate's conservatism is transparent.
- **loc-public-domain-engine-screen-002**
  - Every cleared item is screened; TK-label / sensitive / living-person hits are **held for review**,
    not fanned out.

**M1 Definition of Done:** one approved source cleared end-to-end with 100% provenance; stratified
independent rights audit shows **zero confirmed wrong-clears**; quarantine ledger published;
cultural-sensitivity screen run with flagged items held; polite-protocol compliance demonstrated (cache
hit-rate + zero breaches); ≥1 candidate downstream consumer/steward in conversation.

---

## Milestone M2 — Fan-out contract + first downstream lane

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| loc-public-domain-engine-contract-001 | Define + validate the "cleared item" JSON-LD fan-out contract (idempotent/dedup-keyed) | design-spec | medium | low | document | loc-public-domain-engine-prov-001 | Maintainer |
| loc-public-domain-engine-adapter-001 | Adapter: cleared items → a downstream lane (alt-text or transcription) | code | medium | medium | pr | loc-public-domain-engine-contract-001, loc-public-domain-engine-data-001 | Maintainer + downstream lane reviewer |
| loc-public-domain-engine-ttl-001 | Re-verification (determination TTL) job for stale clears | code | small | medium | pr | loc-public-domain-engine-prov-001 | Rights reviewer |
| loc-public-domain-engine-docs-001 | Consumer guide: contract, attribution, jurisdiction, license-basis | writing | small | low | document | loc-public-domain-engine-contract-001 | Maintainer |

**Acceptance criteria (key M2 tasks)**

- **loc-public-domain-engine-contract-001**
  - JSON-LD contract carries: item reference, media type(s), detected language(s), suggested
    downstream lane(s), provenance-manifest pointer, rights basis + jurisdiction, and the required
    **courtesy attribution** line.
  - Validates against a published JSON Schema; **idempotent** and dedup-keyed by LoC item ID + content
    hash (a re-run never emits a duplicate record).
- **loc-public-domain-engine-adapter-001**
  - One downstream Hee-Lee Oss project (e.g. `a11y-alttext-commons` or a transcription lane) **consumes the
    feed** and receives correctly-attributed, rights-cleared items.
  - Rights basis, jurisdiction, and any CC-BY-SA share-alike obligation are propagated into the
    downstream intake; high-stakes downstream content inherits that lane's expert review + "not advice".
- **loc-public-domain-engine-ttl-001**
  - Items whose determination TTL has expired are re-verified against current LoC metadata before
    re-publication; a changed rights status pulls the item from the cleared set and logs it.

**M2 Definition of Done:** the JSON-LD cleared-item contract finalized + schema-validated +
idempotent; ≥1 downstream adapter built and **one downstream Hee-Lee Oss project consuming the feed**;
attribution/jurisdiction/license-basis propagated; TTL re-verification job operational.

---

## Milestone M3 — Multi-lane fan-out + downstream delivery (shipped)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| loc-public-domain-engine-adapter-002 | Wire a 2nd downstream lane (translation or dataset) | code | medium | medium | pr | loc-public-domain-engine-adapter-001 | Maintainer + downstream lane reviewer |
| loc-public-domain-engine-data-002 | Scale cleared corpus to ≥5,000 items across ≥2 approved sources (100% provenance) | data | large | medium | dataset | loc-public-domain-engine-adapter-001, loc-public-domain-engine-rights-001 | Rights reviewer |
| loc-public-domain-engine-partner-003 | Secure committed consumer/steward + document LoC Labs outcome | research | medium | low | document | loc-public-domain-engine-partner-002 | Maintainer |
| loc-public-domain-engine-sustain-001 | Sustainability: versioned vocab/policy review, reviewer rotation, throughput ceiling | writing | small | low | document | loc-public-domain-engine-partner-003 | Maintainer |

**Acceptance criteria (key M3 tasks)**

- **loc-public-domain-engine-data-002**
  - ≥2 approved sources integrated; ≥5,000 cleared items emitted; **100% provenance** maintained.
  - A fresh stratified rights audit still shows **zero confirmed wrong-clears**.
  - All access remained within LoC's published limits.
- **loc-public-domain-engine-partner-003**
  - A named downstream consumer or external steward commits to adopt and sustain the feed.
  - **≥1 downstream project actually ships artifacts** derived from the feed to beneficiaries.
  - LoC Labs engagement outcome documented honestly (incl. "no response").

**M3 Definition of Done (project "shipped"):** ≥2 downstream lanes wired; **≥1 downstream project has
delivered artifacts** to beneficiaries; ≥5,000 cleared items with 100% provenance and zero confirmed
wrong-clears in a fresh audit; committed consumer/steward secured; LoC Labs outcome documented;
sustainability + reviewer-rotation plan in effect.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| loc-public-domain-engine-adapter-003 | Adapter → `caption-commons` for cleared AV items | code | medium | medium | pr | AV transcripts/captions lane |
| loc-public-domain-engine-bythepeople-001 | Contribute corrected transcriptions back to "By the People" | data | medium | medium | dataset | Align, don't duplicate; needs program agreement |
| loc-public-domain-engine-iiif-001 | IIIF manifest alignment for image-heavy collections | code | medium | low | pr | Improves commons interoperability |
| loc-public-domain-engine-lang-001 | Language detection + routing for non-English items | code | small | low | pr | Routes to translation lane |
| loc-public-domain-engine-runner-001 | Funded-lane OCR pass for machine-print PD books (budget-capped) | code | large | medium | pr | `funded` lane; hard `fundedBudgetUsd` cap |
| loc-public-domain-engine-quality-001 | Automated anomaly flagging for the rights audit (assistive) | code | medium | low | pr | Human-confirmed; never auto-clears |
| loc-public-domain-engine-dashboard-001 | Public metrics dashboard (clears, quarantine reasons, cache hit-rate) | code | small | low | pr | Transparency surface |

---

## Example task JSON

Schema-valid Task JSON for the first M0 task (`loc-public-domain-engine-rights-001`):

```json
{
  "id": "loc-public-domain-engine-rights-001",
  "title": "Rights-vocabulary mapping + eligibility allow-list (deny-by-default)",
  "project": "loc-public-domain-engine",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["open-culture", "public-data", "digital-libraries", "public-domain", "accessibility"],
  "riskTier": "medium",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "The LoC public-domain engine fans cleared items into downstream good-deed tasks, but the Library of Congress explicitly does not make rights determinations for users -- the legal assessment is the reuser's responsibility. So the rights-gate is the product, and it must be conservative: deny by default. This task defines the mapping from LoC / rightsstatements.org / Creative Commons rights values to an eligibility decision, before any item is fetched at scale or fanned out. See PLAN.md (Data, licensing & compliance).",
  "objective": "Define rights/vocabulary.yml mapping each rights value to eligible | ineligible | needs-review with a recorded rationale and jurisdiction, such that only an affirmative public-domain/open determination (recognized rights statement, CC0/open CC, or unambiguous pre-1929-by-date) fans out, and everything ambiguous is quarantined.",
  "acceptanceCriteria": [
    "Every LoC / rightsstatements.org / Creative Commons rights value used is mapped to eligible | ineligible | needs-review with a written rationale.",
    "Deny by default: any value not affirmatively listed as eligible resolves to ineligible; borderline values resolve to needs-review for human adjudication.",
    "Pre-1929-by-date eligibility is allowed only with an affirmative, unambiguous publication date in the item's own metadata; date inference to fill a gap is explicitly forbidden.",
    "Each determination records its jurisdiction (default U.S.) and the rule that produced it.",
    "The ruleset is reviewed and signed off by counsel / a qualified rights reviewer before any use.",
    "A golden-test corpus of known items per category (including negative cases that must be quarantined) is enumerated for CI."
  ],
  "resources": [
    "planning/projects/loc-public-domain-engine/PLAN.md",
    "https://www.loc.gov/legal/",
    "https://rightsstatements.org/",
    "https://creativecommons.org/licenses/",
    "https://www.loc.gov/apis/"
  ],
  "output": "A counsel-reviewed rights/vocabulary.yml mapping plus a human-readable rights-determination policy document and an enumerated golden-test corpus, committed via PR.",
  "requestor": "jdev1977",
  "verifiedNeed": false,
  "outputLicense": "CC0-1.0"
}
```

---

## Generated task index

All backlog rows above have been decomposed into schema-valid `tasks/<id>.json` files.
Generated: 2026-06-29. Validator: `validate-tasks.mjs`. Result: **27/27 PASS**.

| File | Milestone | Type | Lane | Priority |
| --- | --- | --- | --- | --- |
| tasks/loc-public-domain-engine-rights-001.json | M0 | design-spec | donated | high |
| tasks/loc-public-domain-engine-policy-001.json | M0 | research | donated | high |
| tasks/loc-public-domain-engine-client-001.json | M0 | code | donated | high |
| tasks/loc-public-domain-engine-prov-001.json | M0 | design-spec | donated | high |
| tasks/loc-public-domain-engine-screen-001.json | M0 | design-spec | donated | high |
| tasks/loc-public-domain-engine-ci-001.json | M0 | code | donated | high |
| tasks/loc-public-domain-engine-partner-001.json | M0 | research | donated | high |
| tasks/loc-public-domain-engine-data-001.json | M1 | data | donated | high |
| tasks/loc-public-domain-engine-audit-001.json | M1 | research | donated | high |
| tasks/loc-public-domain-engine-ledger-001.json | M1 | data | donated | high |
| tasks/loc-public-domain-engine-screen-002.json | M1 | research | donated | high |
| tasks/loc-public-domain-engine-partner-002.json | M1 | research | donated | high |
| tasks/loc-public-domain-engine-contract-001.json | M2 | design-spec | donated | medium |
| tasks/loc-public-domain-engine-adapter-001.json | M2 | code | donated | medium |
| tasks/loc-public-domain-engine-ttl-001.json | M2 | code | donated | medium |
| tasks/loc-public-domain-engine-docs-001.json | M2 | writing | donated | medium |
| tasks/loc-public-domain-engine-adapter-002.json | M3 | code | donated | medium |
| tasks/loc-public-domain-engine-data-002.json | M3 | data | donated | medium |
| tasks/loc-public-domain-engine-partner-003.json | M3 | research | donated | medium |
| tasks/loc-public-domain-engine-sustain-001.json | M3 | writing | donated | medium |
| tasks/loc-public-domain-engine-adapter-003.json | Backlog | code | donated | low |
| tasks/loc-public-domain-engine-bythepeople-001.json | Backlog | data | donated | low |
| tasks/loc-public-domain-engine-iiif-001.json | Backlog | code | donated | low |
| tasks/loc-public-domain-engine-lang-001.json | Backlog | code | donated | low |
| tasks/loc-public-domain-engine-runner-001.json | Backlog | code | funded | low |
| tasks/loc-public-domain-engine-quality-001.json | Backlog | code | donated | low |
| tasks/loc-public-domain-engine-dashboard-001.json | Backlog | code | donated | low |
