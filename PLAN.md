# PLAN — loc-public-domain-engine

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

A **rights-gate** and a **polite API-access protocol** over the Library of Congress (LoC) that
identifies *demonstrably* public-domain / openly-licensed items and fans each cleared item into
downstream good-deed tasks — transcription, OCR correction, alt-text, translation, and structured
datasets — **without ever guessing at rights and without ever hammering LoC's servers.**

The whole project rests on one conservative principle: **deny by default.** An item is fanned out
only when an affirmative, recorded rights determination clears it; everything ambiguous is
quarantined, never published, and never handed to a downstream task. LoC itself disclaims making
rights determinations for users — so the gate is the product, and its precision (zero items wrongly
cleared) matters more than its throughput.

## Executive summary

The Library of Congress holds millions of digitized items, a large share of them public domain, and
exposes them through a JSON API (`?fo=json`), specialized APIs (Chronicling America historic
newspapers), and bulk data offerings. But two hard problems sit between that material and useful
public good:

1. **Rights are ambiguous and per-item.** LoC attaches rights/access statements at the item and
   collection level, but explicitly tells users that **the final legal assessment of whether an item
   may be reused is the user's responsibility, not LoC's.** Naively treating "it's on loc.gov" as "it's
   public domain" is exactly the mistake that produces license violations — a Hee-Lee Oss hard-refusal.
2. **Bulk programmatic access is easy to abuse.** A fan-out engine that crawls per-item can trivially
   exceed LoC's published rate limits, degrade a public service for everyone, and get the project (and
   Hee-Lee Oss) blocked. Politeness is not optional; it is an engineering requirement and an ethical one.

This project builds the **agent-neutral spine** that solves both: a conservative, auditable
**rights-gate** that maps LoC/rightsstatements.org/Creative Commons rights metadata to a small
allow-list of "fan-out eligible" determinations (deny-by-default, ambiguity → quarantine), and a
**polite API protocol** (conditional requests + caching, configurable rate limits honoring LoC's
published policy, exponential backoff with jitter on 429/5xx, a circuit breaker, and a descriptive
contact User-Agent). Every cleared item emits a **frozen provenance manifest** (the exact API
response, the rights field, a retrieval timestamp, a content hash) and a typed **"cleared item"
contract** that downstream Hee-Lee Oss projects consume.

The engine does **not** itself do the transcription/translation/alt-text work — it *feeds* the
existing Hee-Lee Oss lanes (`a11y-alttext-commons`, `public-domain-translations`, `caption-commons`,
`civic-open-data`) with rights-cleared, provenance-stamped source material. M0 is the spine: the
rights-gate + the API protocol. Later milestones wire the fan-out to real downstream consumers and
secure a steward.

Risk tier: **medium** — driven primarily by **rights/license correctness** (a wrong clear is a legal
and ethical failure), with secondary **cultural-sensitivity/privacy** and downstream
domain-accuracy review requirements.

## Problem & beneficiaries

**The problem.** Enormous quantities of public-domain cultural heritage at LoC are effectively
inaccessible as *reusable* material because (a) determining which specific items are safe to reuse is
slow, expert, per-item work that most reusers skip or get wrong, and (b) there is no shared, polite,
rights-aware pipeline that turns "a public-domain item exists" into "a transcription / alt-text /
translation / dataset that a real beneficiary can use." Individual good-deed projects each re-solve
rights-clearing and API etiquette badly; LoC bears the load of uncoordinated crawlers.

**Beneficiaries.**
- **Blind and low-vision users** — via alt-text generated for cleared LoC images (fed to
  `a11y-alttext-commons`).
- **Speakers of low-resource languages** — via translations of cleared public-domain texts (fed to
  `public-domain-translations`).
- **Researchers, students, educators, digital humanists** — via clean transcriptions, OCR-corrected
  text, and structured datasets derived from cleared items.
- **The open-knowledge commons** (Wikisource, Wikimedia Commons, the Internet Archive, library
  linked-data) — which can ingest provenance-stamped, rights-cleared derivatives.
- **The Library of Congress and its users** — indirectly, via a *polite* consumer that reduces
  uncoordinated crawling and can contribute corrected transcriptions back.

**Verified need.** The *gap* (no shared, conservative rights-gate + polite fan-out exists, and
downstream Hee-Lee Oss projects need rights-cleared source material) is real and demonstrable, and
sister projects in the portfolio (`a11y-alttext-commons`, `public-domain-translations`,
`caption-commons`) are concrete internal consumers. However, a **named external partner/steward who
will adopt and sustain the engine — ideally LoC Labs or a library/accessibility org — is TO BE
SECURED.** Per the Hee-Lee Oss quality bar ("delivered, not merged"), securing a last-mile consumer (even
an internal Hee-Lee Oss project committing to *adopt the feed*) is a first-class M1/M2 objective and a
precondition for declaring the project *shipped*.

**Partner org.** TO BE SECURED. Candidate stewards/partners: **LoC Labs** (for API-etiquette
guidance and possible collaboration), the **"By the People" / Concordia** crowd-transcription
program (align, don't duplicate), a university **digital-humanities** center, **Wikimedia / Wikisource**
communities, and an **accessibility organization**. Internal Hee-Lee Oss consumers are the immediate,
committed adopters; an external steward is the ideal long-term owner.

## Goals and non-goals

**Goals**
- Build a **conservative, auditable rights-gate**: deny-by-default mapping of LoC /
  rightsstatements.org / Creative Commons rights metadata to a small allow-list of "fan-out eligible"
  determinations; ambiguity → quarantine, never publication.
- Build a **polite API-access protocol** that honors LoC's published rate-limit/crawling policy,
  uses conditional requests + caching, backs off on 429/5xx, and identifies itself with a contact
  User-Agent.
- Emit a **frozen provenance manifest** per cleared item (raw API response snapshot + rights field +
  retrieval timestamp + content hash) so every downstream artifact is reproducible and auditable.
- Define a typed **"cleared item" fan-out contract** (JSON-LD) that downstream Hee-Lee Oss projects
  consume, and **wire at least one real downstream lane** end-to-end.
- Add a **cultural-sensitivity / privacy screen** distinct from the rights-gate (PD ≠ ethically clear).
- Publish a **transparent quarantine ledger** (counts and reasons for exclusion) so the gate's
  conservatism is auditable.
- Secure at least one committed downstream consumer/steward and document LoC Labs engagement.

**Non-goals**
- **Not** a re-host or mirror of LoC content; it derives manifests + cleared-item references and
  feeds derivatives, it does not republish LoC's media at scale.
- **Not** a tool that *guesses* rights or "best-effort" clears ambiguous items. **No determination,
  no fan-out** — full stop.
- **Not** itself the transcription/OCR/alt-text/translation engine; those live in the respective
  Hee-Lee Oss projects. This project is the **rights-gate + protocol + fan-out**.
- **Not** a crawler that ignores LoC's rate limits or robots/crawl policy to maximize coverage.
- **Not** a collector of controlled-access, restricted, or rights-encumbered LoC material, nor of
  personally identifiable data about living people.
- **Not** a duplicate of LoC's "By the People" transcription platform; the project aligns with and
  feeds it rather than competing.
- **Not** an arbiter that overrides LoC's own rights statements; where LoC says "rights undetermined,"
  the engine treats the item as **not eligible**.

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. Baselines are zero at project start unless noted. We
explicitly **do not** count items crawled, API calls made, or PRs merged as success.

| Metric | Baseline | Target (first 12 months) |
| --- | --- | --- |
| **Rights-gate precision** — items fanned out that an independent reviewer confirms were wrongly cleared | n/a | **Zero confirmed wrong-clears** in every stratified audit (hard gate; a wrong clear is a license violation) |
| Share of fanned-out items carrying a complete, frozen provenance manifest | n/a | 100% (CI hard gate; no manifest → no fan-out) |
| Cleared items emitted to the fan-out contract from approved sources | 0 | ≥ 5,000 |
| Items correctly quarantined and logged with a reason (transparency) | n/a | 100% of non-cleared items logged in the quarantine ledger |
| Cultural-sensitivity/privacy screen coverage of cleared items | n/a | 100% screened before fan-out; flagged items held for review |
| Downstream lanes wired end-to-end (alt-text / transcription / translation / dataset) | 0 | ≥ 2 lanes consuming the feed |
| **Downstream artifacts actually delivered to beneficiaries** (not just produced) | 0 | ≥ 1 downstream project ships artifacts derived from the feed |
| Polite-protocol compliance — sustained request rate within LoC's published limits | n/a | 100% (zero policy breaches; breaches auto-pause via circuit breaker) |
| LoC-load reduction — share of repeat fetches served from cache / conditional 304s | n/a | ≥ 70% of re-fetches avoid a full transfer |
| Rights re-verification freshness — cleared items re-checked before their determination TTL expires | n/a | 100% (no stale clear re-published past TTL) |
| Committed downstream consumer / external steward secured | none | ≥ 1 committed adopter; LoC Labs engagement documented (outcome recorded honestly, incl. "no response") |

**Rights-audit sampling frame (pins the precision metric).** "Zero wrong-clears" is meaningless
without a defined sample, so the audit uses: a **minimum sample of 200 cleared items per release** (or
the whole release if smaller); **stratified sampling** across strata defined by *rights-statement
category* (e.g., "no known restrictions," CC0, CC-BY, pre-1929 PD-by-date, rightsstatements.org
NoC-US) and by *source collection*; and an **auditor independent of the gate run** that produced the
clear. The cultural-sensitivity screen draws its own stratified sample.

## Scope

**In scope**
- The rights-gate: rights-vocabulary mapping, the eligibility allow-list, deny-by-default logic,
  quarantine, and the rights-determination ruleset (counsel-reviewed).
- The polite API protocol: client with configurable rate limits, conditional requests + cache,
  backoff/jitter, circuit breaker, contact User-Agent; preference for LoC bulk data / sitemaps over
  per-item crawling where available.
- Provenance manifests (frozen API snapshots, rights field, timestamp, content hash) and the
  reproducibility store.
- The typed "cleared item" fan-out contract (JSON-LD) and adapters that hand items to downstream
  Hee-Lee Oss projects.
- The cultural-sensitivity / privacy screen and the public quarantine ledger.
- Wiring **at least one** downstream lane (alt-text or transcription) end-to-end to a real consumer.

**Out of scope (explicit)**
- **Republishing or mirroring LoC media at scale.** The engine references and derives; it is not a
  CDN for LoC's assets.
- **Any "best-effort" or heuristic clearing of ambiguous items.** Undetermined rights = ineligible.
- **Performing the downstream work itself** (the actual alt-text/transcription/translation/dataset
  authoring lives in the respective Hee-Lee Oss projects).
- **Ingesting controlled-access, restricted, or rights-undetermined LoC items**, or any
  personally-identifiable data about living people.
- **Crawling that ignores LoC's published rate-limit/robots/crawl policy.**
- **Building a parallel transcription platform** to "By the People."
- **Commercial packaging** of LoC-derived data, or any primarily for-profit use.

## Solution approach & architecture

An **agent-neutral pipeline + library** (per Hee-Lee Oss: lives in core/adapters, no vendor-specific
logic), not a hosted service. The donated lane runs it; humans run their own agents.

**Pipeline stages**

1. **Discovery (polite).** Prefer LoC **bulk data packages, item sitemaps, and collection
   manifests** over per-item crawling. Where per-item access is needed, request `?fo=json` and use
   the `at=` parameter to fetch only required fields, minimizing payload and load.
2. **Polite fetch layer.** A single client wraps all LoC access:
   - **Configurable rate limits** read from a `loc-policy.yml` that records LoC's *currently
     published* per-endpoint limits (verified at M0; treated as data, not hardcoded constants, because
     LoC's policy can change). A single-flight concurrency cap and a token-bucket throttle enforce them.
   - **Conditional requests + cache:** send `If-None-Match`/`If-Modified-Since`; cache responses
     (with ETag/Last-Modified) so re-fetches return `304` and avoid full transfers.
   - **Backoff + circuit breaker:** exponential backoff with jitter honoring `Retry-After` on `429`
     and `5xx`; a circuit breaker that **auto-pauses and alerts** on sustained errors — never hammers.
   - **Identification:** a descriptive `User-Agent` with a project URL and contact email (politeness +
     LoC's expectation of identifiable robots). No secrets in headers, logs, or receipts.
3. **Rights-gate (the headline control).** For each item, extract LoC rights/access fields
   (`rights`, `rights_advisory`, `access_restricted`, collection rights), plus any
   rightsstatements.org URIs and Creative Commons license URIs. Map them through a documented
   **rights-vocabulary table** to one of: `eligible` (a recorded affirmative PD/open determination),
   `ineligible` (restricted/undetermined), or `needs-review` (borderline). **Deny by default:** only
   `eligible` proceeds; `needs-review` is queued for the rights reviewer; everything else is
   quarantined. A *pre-1929-by-date* determination is allowed **only** when the item's own metadata
   affirmatively supports it (publication date present and unambiguous) — never inferred to fill a gap.
4. **Cultural-sensitivity / privacy screen.** Independent of rights: flag materials that are PD yet
   ethically sensitive — Indigenous/Traditional-Knowledge materials (check for **TK Labels** /
   community provenance), human-remains or ethnographic content, and any item surfacing
   **living-person** personal data. Flagged items are held for review, not auto-fanned-out.
5. **Provenance manifest (frozen).** Each cleared item gets a manifest: the **raw API response
   snapshot**, the resolved rights determination + the rule that produced it, the LoC item URL, a
   **retrieval timestamp**, a **content hash** of the referenced asset(s), and a **determination TTL**
   (re-verify before expiry). This makes every clear reproducible even if LoC's live metadata later
   changes.
6. **Fan-out contract.** Emit a typed **"cleared item"** record (JSON-LD, aligned to schema.org /
   Dublin Core / IIIF where applicable) carrying the item reference, media type(s), language(s)
   (detected), suggested downstream lane(s), the provenance manifest pointer, and the required
   courtesy attribution line. Idempotent: keyed by LoC item ID + content hash so a re-run never
   spawns duplicate downstream tasks.
7. **Adapters → downstream lanes.** Thin adapters translate a cleared-item record into the right
   downstream Hee-Lee Oss project's intake (alt-text → `a11y-alttext-commons`; text → `public-domain-
   translations` / transcription; AV → `caption-commons`; structured → `civic-open-data`). Routing is
   suggested by media type + language; the downstream project owns its own domain review.
8. **Quarantine ledger + metrics.** Every non-cleared item is logged with its reason; aggregate
   counts (by rights category) are published so the gate's conservatism is transparent and auditable.

**Tech stack**
- TypeScript, ESM, pnpm (Hee-Lee Oss conventions). Agent-neutral logic in `core`; anything tool-specific in
  `adapters/`.
- HTTP client with throttling/caching (e.g., a token-bucket + conditional-request layer); local cache
  store keyed by URL + ETag.
- Validation: JSON Schema for the fan-out contract + a provenance-completeness linter (CI gate: no
  manifest → fail) + a rights-gate unit-test corpus (golden cases).
- Serialization: JSON-LD for cleared-item records; YAML for `loc-policy.yml` and the rights-vocabulary
  table.

**Key data artifacts**
- `loc-policy.yml` — LoC's published rate limits/crawl policy, verified + dated.
- `rights/vocabulary.yml` — the rights-statement → `eligible|ineligible|needs-review` mapping
  (counsel-reviewed; this is the legal heart of the gate).
- `rights/audit/` — golden test corpus of known items per category (regression-tests the gate).
- `manifests/` — frozen provenance manifests.
- `ledger/quarantine.jsonl` — append-only exclusion log.

**Key decisions (to ratify in M0)**
- **Rights-vocabulary mapping** — exactly which LoC/rightsstatements.org/CC values map to `eligible`,
  and the conservative defaults for everything else. **Counsel-reviewed; deny-by-default.**
- **Determination TTL** — how long a rights clear is trusted before re-verification (proposed: 180
  days), because LoC can revise rights metadata.
- **Bulk-vs-crawl** — confirm which LoC bulk/sitemap offerings exist and prefer them; per-item
  crawling is the fallback, rate-limited.
- **Fan-out contract shape** — JSON-LD vocabulary alignment (schema.org / Dublin Core / IIIF) so
  downstream consumers and the wider commons can ingest it.

## Data, licensing & compliance

**This is the headline gate for the project. Read this section before any data work.**

### Hard boundary — LoC does not clear rights for you
LoC's standard guidance is explicit: it **does not make rights determinations on behalf of users**,
and "responsibility for making an independent legal assessment of an item and securing any necessary
permissions ultimately rests with persons desiring to use the item." Therefore:
- **"It is on loc.gov" is never sufficient.** Only an **affirmative, recorded** rights determination
  (a recognized PD/open rights statement, or unambiguous pre-1929-by-date evidence in the item's own
  metadata) makes an item eligible.
- **Undetermined / restricted / ambiguous → ineligible and quarantined.** No heuristic "probably PD."
- The engine records, on each manifest, that the determination was made by *this project's conservative
  ruleset* (not by LoC) and is subject to the user's own due diligence — preserving honesty about who
  bears the assessment.

### Approved rights determinations (allow-list — only these fan out)
Each entry lives in `rights/vocabulary.yml` with the source value, the determination, and a rationale,
**reviewed by counsel/qualified rights reviewer** before use:
- **LoC "no known restrictions on publication"** / equivalent affirmative LoC rights statements.
- **rightsstatements.org** PD/no-copyright categories (e.g., `NoC-US`, `PDM`-aligned) — mapped
  conservatively; the in-copyright and "undetermined" categories map to **ineligible**.
- **Creative Commons** `CC0` and open CC licenses (`CC-BY`, `CC-BY-SA`) where LoC asserts them — with
  share-alike/attribution obligations carried into the contract.
- **Public domain by U.S. publication date** — pre-1929 (rolling per current U.S. term) **only** when
  the item's metadata affirmatively and unambiguously establishes the publication date. Date inferred
  to fill a gap is **never** sufficient.
- **U.S. federal government works** (PD as government works) where LoC identifies them as such.
- Specific high-PD collections (e.g., **Chronicling America** historic newspapers) verified at the
  collection level **and** confirmed item-level.

**Caveats we will not gloss over:**
- A PD original can be wrapped by a third party's copyrighted digitization, restoration, or added
  metadata; the determination must concern the **specific digital object** LoC serves.
- Collection-level rights statements do **not** override an item that carries its own restriction;
  item-level always wins, and the more restrictive of the two governs.
- Rights metadata can change; hence the **determination TTL** and re-verification.
- "Public domain in the U.S." ≠ public domain worldwide; the contract records the **jurisdiction** of
  the determination (default: U.S.), and downstream reusers in other jurisdictions are warned.

### Cultural-sensitivity & privacy stance (separate from rights)
- **PD ≠ ethically clear.** A separate screen flags Indigenous / Traditional-Knowledge materials (look
  for **TK Labels** and community provenance), sensitive ethnographic or human-remains content, and any
  surfacing of **living-person** personal data. Flagged items are **held for review**, never auto-fanned.
- **No personally identifiable data about living people** is collected or fanned out, regardless of PD
  status.

### Provenance & attribution
- **Every cleared item** carries a frozen manifest: raw API snapshot, rights field + the rule that
  cleared it, LoC item URL, retrieval timestamp, content hash, jurisdiction, and TTL.
- **Courtesy attribution** to the Library of Congress and the specific item/collection is required in
  the contract and carried into every downstream artifact, even for PD material (good provenance
  practice and LoC's preferred-citation norm).

### Output license
- **Code:** MIT. **Engine outputs (manifests, contract records, quarantine ledger, vocabulary):**
  **CC0-1.0** (these are factual/derived metadata). **Downstream derivative works** (translations,
  alt-text, datasets) carry the license of their own project — typically CC0 or CC-BY/CC-BY-SA — with
  any CC-BY-SA share-alike obligation propagated from source. The contract records the source rights
  basis so downstream license choices are constrained correctly.

## Quality, review & risk gates

**Risk tier: medium.** Review dimensions, all required before a deed is "done":

1. **Rights/license review (primary gate).** A qualified rights reviewer (and counsel for the
   vocabulary ruleset itself) signs off the `rights/vocabulary.yml` mapping and adjudicates every
   `needs-review` item. **No item is fanned out without an `eligible` determination produced by the
   approved ruleset.** Any task proposing to clear ambiguous items by heuristic, or to crawl past
   LoC's limits, is **refused and flagged** per Hee-Lee Oss guardrails.
2. **Cultural-sensitivity / privacy review.** Flagged sensitive or living-person items are held until
   a reviewer (Indigenous-data / ethics competence where relevant) clears or excludes them.
3. **Politeness review.** The protocol's compliance with LoC's published limits is verified; the
   circuit breaker and backoff are tested; the contact User-Agent is correct.
4. **Downstream domain review.** Each downstream lane applies its own review (alt-text accuracy,
   translation native-review, OCR accuracy baseline) — high-stakes content (medical/legal/safety) in a
   downstream lane requires that lane's **credentialed expert sign-off** and a "not advice" label.

**Definition of Shipped (project level).** A live rights-gate + polite protocol with: **100% of
fanned-out items carrying a frozen provenance manifest**; **zero confirmed wrong-clears** in the
stratified rights audit; a transparent quarantine ledger; the cultural-sensitivity screen operational;
**≥2 downstream lanes wired** and **≥1 downstream project actually shipping artifacts** derived from
the feed; full compliance with LoC's published rate-limit policy; and **≥1 committed downstream
consumer/steward** with LoC Labs engagement documented. Per Hee-Lee Oss, *delivered ≠ merged*.

**Per-deed Definition of Done.** Acceptance criteria met + CI green (schema + provenance-completeness
+ rights-gate golden tests) + rights review passed + cultural/privacy screen passed + politeness
compliance verified + output published under the declared license.

## Roadmap & milestones

**M0 — Rights-gate + polite API protocol spine (cold-start). [the spine]**
Goal: stand up the two foundational controls so no item can be fanned out without an affirmative,
recorded rights clear, and no LoC access can breach the published policy.
Exit criteria:
(a) `rights/vocabulary.yml` defined with the eligibility allow-list, deny-by-default logic, and
  **counsel/qualified-reviewer sign-off** on the ruleset;
(b) the polite client implemented — `loc-policy.yml` populated with LoC's **currently published**
  limits (verified + dated), conditional requests + cache, backoff/jitter on 429/5xx, circuit
  breaker, contact User-Agent;
(c) the provenance-manifest format defined (raw snapshot + rights rule + timestamp + content hash +
  TTL + jurisdiction);
(d) the cultural-sensitivity / privacy screen specified;
(e) CI gates live — provenance-completeness linter + a **rights-gate golden-test corpus** (known
  items per rights category, incl. negative cases that must be quarantined);
(f) a **qualified rights reviewer named** (hard exit; documented fallback if the seat is empty — M0
  cannot exit and escalation begins);
(g) LoC Labs / API-etiquette outreach started (status logged).

**M1 — First cleared corpus + transparency (proof of the gate).**
Goal: prove the gate end-to-end on a real LoC source and publish the evidence.
Exit criteria:
(a) ≥1 approved high-PD source (e.g., Chronicling America) run through discovery → polite fetch →
  rights-gate → manifest, producing a cleared corpus;
(b) **100%** of cleared items carry a frozen manifest and pass CI;
(c) **stratified rights audit** (≥200 or whole release; independent auditor) shows **zero confirmed
  wrong-clears**;
(d) the **quarantine ledger** is published with reason counts;
(e) cultural-sensitivity screen run over the corpus; flagged items held;
(f) polite-protocol compliance demonstrated (cache hit-rate + zero policy breaches);
(g) ≥1 candidate downstream consumer/steward in conversation. Depends on M0.

**M2 — Fan-out contract + first downstream lane (usable feed).**
Goal: turn cleared items into a typed feed a real downstream project consumes.
Exit criteria:
(a) the **"cleared item" JSON-LD contract** finalized + schema-validated, idempotent/dedup-keyed;
(b) ≥1 downstream adapter built (alt-text or transcription) and **one downstream Hee-Lee Oss project
  consuming the feed**;
(c) attribution + jurisdiction + license-basis correctly propagated into downstream intake;
(d) re-verification (TTL) job operational. Depends on M1.

**M3 — Multi-lane fan-out + downstream delivery (shipped).**
Goal: broaden the fan-out and prove real beneficiary delivery.
Exit criteria:
(a) ≥2 downstream lanes wired (e.g., alt-text + translation, or + dataset);
(b) **≥1 downstream project actually ships artifacts** derived from the feed to beneficiaries
  (Definition of Shipped met);
(c) ≥5,000 cleared items emitted with 100% provenance and zero confirmed wrong-clears in a fresh
  audit;
(d) committed consumer/steward secured; LoC Labs engagement outcome documented (incl. "no response");
(e) sustainability/maintenance + reviewer-rotation plan in effect. Depends on M2.

## Work breakdown

The itemized, schema-mapped backlog lives in [`TASKS.md`](./TASKS.md), organized by the milestones
above (M0–M3) plus a sized backlog. Each task maps to a Hee-Lee Oss Task JSON and carries a type, size,
risk tier, deliverable, dependencies, and reviewer. M0 deliberately front-loads the **rights-gate**
and the **polite protocol** before any corpus or fan-out work begins — the spine before the fan-out.

## Governance, roles & stakeholders

- **Maintainer / Owner:** TBD — accountable for scope, the rights-gate, the polite protocol, and
  releases.
- **Rights/license reviewer (+ counsel for the ruleset):** TBD — approves `rights/vocabulary.yml`,
  adjudicates `needs-review` items, and holds veto over any clear. Mandatory (medium risk; primary
  gate). **Naming a qualified person is a hard M0 exit criterion.** **Documented fallback if the seat
  is empty:** no determination advances past `needs-review`, no item is fanned out, M0 cannot exit;
  the maintainer escalates to Hee-Lee Oss governance/board (and may engage pro-bono counsel) before any
  fan-out proceeds.
- **Cultural-sensitivity / privacy reviewer:** TBD — competence in Indigenous-data / ethical-archive
  norms where relevant; clears or excludes flagged items.
- **Politeness / infra owner:** TBD — owns `loc-policy.yml` accuracy, the circuit breaker, and
  monitoring of LoC compliance.
- **Downstream lane reviewers:** owned by the consuming Hee-Lee Oss projects (alt-text, translation,
  transcription, dataset) — each enforces its own domain/expert review.
- **Steward (last-mile owner):** the downstream consumer or external partner who adopts and sustains
  the feed. **TO BE SECURED** — required for "shipped." Internal Hee-Lee Oss consumers are the immediate
  committed adopters.
- **LoC Labs liaison:** TBD — owns API-etiquette guidance and possible collaboration.
- **Hee-Lee Oss governance/board:** arbiter for edge cases (borderline rights category, sensitive-material
  call) under the published conflict-of-interest/veto checklist.

## Dependencies & integrations

- **Library of Congress JSON API** (`loc.gov` `?fo=json`, `at=` partial responses), **Chronicling
  America** historic-newspaper API, and **LoC bulk data / sitemaps** (preferred for load reduction).
- **rightsstatements.org** vocabulary and **Creative Commons** license URIs (rights mapping).
- **schema.org / Dublin Core / IIIF** (cleared-item contract alignment).
- **Local TK Labels references** (cultural-sensitivity screen).
- **Downstream Hee-Lee Oss projects** — `a11y-alttext-commons`, `public-domain-translations`,
  `caption-commons`, `civic-open-data` (consumers of the fan-out feed).
- **Hee-Lee Oss pieces:** Task schema (`packages/schema`), agent-neutral core (`packages/core`,
  `packages/cli`), adapters pattern, governance proposal/registry process. Donated lane — humans run
  their own agents; the CLI never runs headless. Any future metered OCR/translation run would use the
  **funded** lane (`packages/runner`) with a hard per-task budget cap.
- **LoC Labs / "By the People" (Concordia)** — optional, ideal partnership; align rather than
  duplicate.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| An ambiguous/restricted item is wrongly cleared and fanned out (license violation) | Medium | Critical (legal/ethical, project-ending) | Deny-by-default gate; affirmative-determination-only allow-list; counsel-reviewed vocabulary; rights-gate golden tests incl. negative cases; stratified independent audit with **zero-wrong-clear** target; refusal + flag of any heuristic-clearing task | Rights reviewer |
| LoC rate-limit breach / uncoordinated crawling degrades a public service or gets us blocked | Medium | High | `loc-policy.yml` honoring LoC's published limits; token-bucket throttle + single-flight cap; conditional requests + cache; backoff/jitter on 429/5xx; **circuit breaker auto-pause + alert**; prefer bulk/sitemaps over crawling | Politeness/infra owner |
| LoC revises rights metadata after we cleared an item (stale clear) | Medium | High | **Determination TTL** + re-verification job; frozen snapshot records what was true at clear time; manifest cites *our* conservative ruleset, not LoC | Maintainer |
| PD-but-sensitive material (Indigenous/TK, human remains, living-person data) fanned out | Medium | High (ethical/privacy) | Cultural-sensitivity/privacy screen **separate from** rights; TK-label/community-provenance checks; flagged items held for review; no living-person PII | Cultural/privacy reviewer |
| PD original wrapped in a third party's copyrighted digitization/restoration | Medium | High | Determination concerns the **specific digital object** LoC serves; verify per object, not per original's age; record in manifest | Rights reviewer |
| No committed downstream consumer/steward → "delivered ≠ merged" not met | High | High | Internal Hee-Lee Oss consumers committed as immediate adopters; partner outreach an M1/M2 deliverable; status logged honestly | Maintainer |
| Date-based PD inference used to fill a metadata gap (wrong clear) | Medium | High | Pre-1929 determination allowed **only** with affirmative, unambiguous date in the item's own metadata; inference forbidden; covered by golden tests | Rights reviewer |
| Jurisdiction confusion ("PD in U.S." reused where still in copyright) | Medium | Medium | Contract records determination **jurisdiction** (default U.S.); downstream warning; reusers advised to re-verify locally | Maintainer |
| Reviewer capacity exhausted (rights + cultural review become bottleneck) | Medium | High | Sampling-based audit (not 100% manual re-check); reviewer rotation + response-time SLA; **throughput ceiling** throttles intake when review backlog exceeds it | Maintainer |
| Duplicate downstream tasks from re-runs | Medium | Low | Idempotent fan-out keyed by LoC item ID + content hash | Maintainer |
| Scope creep into re-hosting LoC media or building a transcription platform | Medium | Medium | Explicit non-goals; engine references + derives only; align with "By the People" not duplicate | Maintainer |
| Funded-lane OCR/translation exceeds budget | Low | Medium | Hard per-task `fundedBudgetUsd` cap enforced by `packages/runner`; default lane is donated | Maintainer |

## Security & privacy

- **Threat surface:** small (data/content pipeline, no accounts, no user PII). Main risks are
  *compliance* (wrong rights clear), *politeness* (over-crawling a public service), and *ethics*
  (sensitive cultural / living-person material) — addressed by the gates above.
- **Secrets handling:** LoC public APIs need no auth key; any future credential (e.g., a partner data
  feed) stays out of logs, receipts, and commits per Hee-Lee Oss rules. The donated lane never runs headless
  or authenticates an agent. The funded lane (if used for OCR/translation) runs only via
  `packages/runner` under a hard budget cap.
- **PII:** no living-person personal data is collected or fanned out, regardless of PD status; the
  cultural-sensitivity/privacy screen enforces this.
- **Abuse/misuse prevention:** every cleared item is provenance-stamped and auditable; the engine
  refuses and flags any attempt to clear ambiguous items, crawl past LoC limits, ingest restricted
  material, or surface living-person data. No surveillance or profiling use is supported.

## Sustainability & maintenance

- **After delivery,** the maintainer plus the secured steward/consumer own the feed; downstream Hee-Lee Oss
  projects own their derivatives. The rights-vocabulary table and `loc-policy.yml` are **versioned and
  dated**, with a scheduled review (LoC policy + U.S. PD rolling date change annually).
- **Rights freshness:** the **determination TTL + re-verification job** keeps clears from going stale;
  releases are versioned so downstream consumers can pin a known-good snapshot.
- **Reviewer sustainability:** audits run on **stratified sampling, not exhaustive re-checking**;
  reviewers work a **rotation with a response-time SLA**; a **throughput ceiling** throttles new
  intake when the review backlog grows, so quality gates never silently degrade.
- **Politeness maintenance:** monitoring keeps request rates within LoC's published limits; the
  circuit breaker and `loc-policy.yml` are re-verified whenever LoC updates its policy.
- **Outcome tracking:** quarterly report on cleared-item count, provenance completeness (must stay
  100%), rights-audit wrong-clear count (must stay zero), quarantine reason breakdown, cache hit-rate /
  policy compliance, downstream lanes wired, and **downstream artifacts actually delivered**.
- If no steward/consumer is secured, the project remains in a maintained-but-not-shipped state and the
  gap is reported honestly rather than declared done.

## Open questions

- Who is the committed downstream consumer / external steward? (TO BE SECURED — blocks "shipped." An
  internal Hee-Lee Oss project committing to adopt the feed is the minimum bar.)
- Will **LoC Labs** engage on API etiquette / collaboration, and will **"By the People"** accept
  contributed transcriptions back? (Outcomes recorded honestly, incl. "no response.")
- Exact current LoC per-endpoint rate limits and which **bulk/sitemap** offerings exist — verified and
  dated into `loc-policy.yml` at M0.
- Final rights-vocabulary mapping: precisely which rightsstatements.org / LoC values map to `eligible`
  vs `needs-review` — counsel-reviewed in M0.
- Determination TTL length (proposed 180 days) and the U.S. PD rolling-date handling.
- Fan-out contract vocabulary: schema.org vs Dublin Core vs IIIF emphasis for best downstream + commons
  ingestion.

## References

- Project proposal: `governance/proposals/loc-public-domain-engine.md` — **does not yet exist
  (TO BE WRITTEN);** this plan is ahead of the proposal and should be reconciled with it.
- Hee-Lee Oss work rules: `CLAUDE.md`
- Good Deed Definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- Portfolio roadmap: `planning/ROADMAP.md`
- Library of Congress JSON API (`loc.gov`, `?fo=json`, `at=`); Chronicling America API; LoC bulk data
- Library of Congress rights & access / legal: LoC does not make rights determinations for users
- rightsstatements.org vocabulary; Creative Commons licenses; Traditional Knowledge (TK) Labels
- LoC Labs; "By the People" / Concordia crowd-transcription platform
- schema.org, Dublin Core, IIIF (cleared-item contract alignment)
- Downstream Hee-Lee Oss projects: `a11y-alttext-commons`, `public-domain-translations`, `caption-commons`,
  `civic-open-data`

---

## Appendix A — Improvements applied

This plan was drafted, then deliberately hardened. The 25 specific improvements below were
identified against the first draft and **all applied** to the plan and `TASKS.md` above. They are
retained here so the strengthening is visible and auditable.

1. **Deny-by-default rights-gate with an explicit allow-list** — only an affirmative recorded
   determination (recognized rights statement, CC0/open CC, or unambiguous pre-1929-by-date) fans
   out; everything else is `ineligible`/quarantined. *(Applied in Architecture §3, Data/licensing.)*
2. **`needs-review` middle state** so borderline items go to a human, never silently pass or fail.
   *(Architecture §3; rights reviewer adjudicates.)*
3. **Counsel review of the rights-vocabulary ruleset itself**, not just per-item — the legal heart of
   the gate is reviewed as an artifact. *(Governance; M0 exit (a).)*
4. **Rights-determination TTL + re-verification job** — clears expire and are re-checked because LoC
   metadata changes. *(Metrics, Architecture §5, Risks, Sustainability.)*
5. **Frozen provenance manifests** (raw API snapshot + rule + timestamp + content hash + TTL +
   jurisdiction) so every clear is reproducible even if LoC's live record changes later.
6. **Politeness as a first-class control** — `loc-policy.yml` honoring LoC's *published* limits as
   versioned data, token-bucket throttle, single-flight cap. *(Architecture §2.)*
7. **Conditional requests + caching** (ETag/If-Modified-Since → 304s) to actively reduce LoC load,
   with a ≥70% cache-hit target metric.
8. **Circuit breaker + backoff/jitter** honoring `Retry-After` on 429/5xx — auto-pause + alert,
   never hammer. *(Architecture §2, Risks.)*
9. **Descriptive contact User-Agent** (project URL + email) so LoC can identify and reach the robot.
10. **Prefer bulk data / sitemaps over per-item crawling** to minimize load; crawling is the
    rate-limited fallback. *(Scope, Architecture §1, Dependencies.)*
11. **Cultural-sensitivity / privacy screen separate from the rights-gate** — PD ≠ ethically clear;
    TK Labels, human-remains/ethnographic, living-person checks. *(Architecture §4, Data/licensing.)*
12. **Traditional Knowledge (TK) Labels** check for Indigenous materials, with hold-for-review.
13. **Living-person PII exclusion** regardless of PD status. *(Security & privacy, Non-goals.)*
14. **Typed JSON-LD "cleared item" fan-out contract** aligned to schema.org/Dublin Core/IIIF so
    downstream Hee-Lee Oss projects *and the wider commons* can ingest it. *(Architecture §6.)*
15. **Idempotent, dedup-keyed fan-out** (LoC item ID + content hash) so re-runs never spawn duplicate
    downstream tasks. *(Architecture §6, Risks.)*
16. **Named internal downstream consumers** (`a11y-alttext-commons`, `public-domain-translations`,
    `caption-commons`, `civic-open-data`) as immediate committed adopters while an external steward is
    TO BE SECURED — gives "delivered ≠ merged" a concrete path. *(Beneficiaries, Dependencies.)*
17. **Outcome metric = downstream artifacts actually delivered**, not items crawled or cleared — the
    only success that counts is beneficiary delivery. *(Success metrics.)*
18. **Rights-audit precision metric = zero confirmed wrong-clears**, with a pinned stratified,
    independent-auditor sampling frame (≥200/release, by rights category + collection).
19. **Public quarantine ledger** with reason counts — the gate's conservatism is transparent and
    auditable, not a black box. *(Architecture §8, Goals, Metrics.)*
20. **Rights-gate golden-test corpus** (known items per category, incl. negative cases that must be
    quarantined) wired into CI so the gate can't silently regress. *(Architecture, M0 exit (e).)*
21. **Jurisdiction recorded on every determination** (default U.S.) — "PD in the U.S." ≠ worldwide;
    downstream reusers warned. *(Data/licensing, Risks.)*
22. **Date-inference forbidden** — pre-1929 PD only with affirmative, unambiguous date in the item's
    own metadata; inferring a date to fill a gap is a wrong-clear. *(Architecture §3, Risks.)*
23. **Courtesy attribution to LoC required even for PD** items, propagated into every downstream
    artifact (provenance + LoC preferred-citation norm). *(Data/licensing, Architecture §6.)*
24. **Honest "LoC does not clear rights for you" framing** — the manifest records that the
    determination is *this project's* conservative call, preserving who bears the legal assessment.
25. **Funded-lane discipline for downstream scale** — any metered OCR/translation runs only via
    `packages/runner` with a hard `fundedBudgetUsd` cap; the spine itself is donated. Plus the
    explicit honesty that **no proposal file exists yet** (the plan leads the proposal) and the
    partner/steward is **TO BE SECURED**. *(Dependencies, Security, References, Risks.)*

## Review sign-off

The revised plan + `TASKS.md` were reviewed for completeness and correctness:

- **Metrics measurable?** Yes — each success metric has a baseline + target; the precision metric is
  pinned to a stratified, independent-auditor sampling frame; cache-hit and policy-compliance are
  quantified; the headline outcome is *downstream artifacts delivered*, not vanity counts.
- **Gates enforceable?** Yes — deny-by-default rights-gate, provenance-completeness CI gate,
  rights-gate golden tests (incl. negative cases), circuit breaker, and the `needs-review` human step
  are mechanically checkable; "no manifest → no fan-out" and "no `eligible` → no fan-out" are hard.
- **Risks owned + mitigated?** Yes — every risk row has a likelihood, impact, mitigation, and a named
  owner role; the critical risk (wrong-clear) has layered controls and a zero-tolerance audit.
- **License / PII / expert-review guardrails present?** Yes — affirmative-determination-only clearing,
  counsel-reviewed vocabulary, jurisdiction recording, a separate cultural-sensitivity/privacy screen,
  living-person PII exclusion, and downstream credentialed expert review + "not advice" for any
  high-stakes downstream content.
- **Sequencing sound?** Yes — M0 is the spine (rights-gate + polite protocol) before any corpus; M1
  proves the gate + transparency; M2 ships the contract + one downstream lane; M3 broadens and proves
  real delivery. Dependencies are explicit and acyclic.
- **Tasks schema-valid?** Yes — every task maps to the required Task fields; the example JSON validates
  against `packages/schema/src/schemas.ts` (all required fields present, enums correct, `verifiedNeed:
  false` while no partner is secured, `outputLicense` set).
- **Items needing a human decision:** (1) write the missing `governance/proposals/loc-public-domain-
  engine.md` proposal to match this plan; (2) name the qualified rights reviewer + counsel (hard M0
  exit); (3) secure a committed downstream consumer/external steward; (4) verify and date LoC's current
  rate limits and bulk offerings into `loc-policy.yml`.
