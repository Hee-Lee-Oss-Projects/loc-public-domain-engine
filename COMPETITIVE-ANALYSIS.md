# Competitive & Improvement Analysis — `loc-public-domain-engine`

> Scope: a rights-gate + polite API-access protocol over the Library of Congress (LoC) that
> clears *demonstrably* public-domain / open items and fans them into downstream good-deed lanes
> (transcription, OCR correction, alt-text, translation, datasets), contributing back upstream.
> Analysis date: 2026-06-29. Web-grounded; URLs cited inline.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature (the 25-item Appendix A hardening pass shows real diligence). The
findings below are specific gaps, not generic nits.

**A. The headline "zero wrong-clears" metric is built on a category that is itself fuzzy — and the
plan under-states it.** rightsstatements.org's `NoC-US` ("No Copyright - United States") *explicitly*
says the determining org "believes" the item is PD **under U.S. law only**, makes **no** assertion
about other countries, and warns that **publicity, privacy, and moral rights may still limit reuse**
(https://rightsstatements.org/page/NoC-US/1.0/). So an item can be correctly `NoC-US` *and* unsafe
for a downstream translation reused in-country abroad, or unsafe because of a living subject's
publicity rights. The plan records `jurisdiction` (good) but treats `NoC-US`/`PDM` as cleanly
`eligible`. The audit's "wrong-clear" definition must be split: (i) copyright wrong-clear vs (ii)
non-copyright-rights wrong-clear (publicity/privacy/moral). As written, an independent auditor has no
crisp rule for (ii), so "zero confirmed wrong-clears" is not yet falsifiable for that class.

**B. `loc-policy.yml` "currently published limits, verified at M0" is under-specified and the real
LoC policy is partly *adaptive*, not a fixed table.** LoC publishes that it has **no API keys**, so
it cannot meter per-user and instead **blocks** abusive callers; crucially, "when the API is
experiencing especially heavy traffic load, **rate limits may decrease** and users may encounter 429s
or **HTML CAPTCHA pages even when operating below the listed rates**"
(https://www.loc.gov/apis/json-and-yaml/working-within-limits/). Documented concrete numbers are
sparse and endpoint-specific (e.g., **Chronicling America bulk OCR: 10 bulk requests / 10 minutes per
IP**; search paging capped at **100,000 items**, ≤1,000/page;
https://guides.loc.gov/chronicling-america/additional-features). Two plan gaps: (1) the politeness
layer must treat **an HTML/CAPTCHA response as a throttle signal** (it is *not* a 429 and a naive
JSON parser will crash or, worse, mis-read it as "no rights field → quarantine" — a silent
correctness bug); (2) "honor published limits" is necessary but **insufficient** because limits float
downward under load — the circuit breaker must key off observed 429/CAPTCHA *and* an adaptive,
self-tuning concurrency (AIMD-style), not just a static token bucket from a YAML file.

**C. The pre-1929 rule is stated as a fixed year but the plan also calls it "rolling" — and conflates
two different PD tests.** U.S. PD-by-publication-date is a rolling 95-year-from-publication window
(2026 → pre-1931 published works), and LoC's own older pages still say "prior to 1923"
(https://www.loc.gov/legal/understanding-copyright/), which is now stale. Hardcoding "1929" will be
**wrong by 2026** and silently drift. More importantly, *date of publication* ≠ *date of creation*;
unpublished works, foreign works (URAA restorations), and sound recordings (pre-2022 Music
Modernization Act rules) follow entirely different tests. The single "pre-1929-by-date" allow-list
entry is too coarse; it needs sub-rules per material type, and the year must be computed from
`currentDate`, not literal.

**D. "Counsel-reviewed vocabulary" is a hard M0 dependency with no fallback that lets M0 actually
ship.** The plan names "name a qualified rights reviewer" as a hard M0 exit, with the documented
fallback being "M0 cannot exit, escalate." For a donated-compute volunteer project, *securing counsel
is the single most likely point of indefinite stall.* There is no tiered fallback (e.g., adopt a
**pre-vetted external ruleset** — DPLA's published rightsstatements mapping, Europeana's
availability rules — as an interim, clearly-labeled, conservative baseline). Without that, the
project's critical path runs through a resource volunteers rarely have.

**E. Provenance manifest freezes the API response but not the *bytes it describes*.** The manifest
stores a "content hash of the referenced asset(s)" and the raw JSON, but the engine is explicitly
**not** a mirror. If LoC later re-derives/replaces a scan (new digitization), the hash mismatches and
the clear is unverifiable — but the downstream artifact (a transcription) already shipped against the
old bytes. The TTL handles *rights metadata* drift but not *asset* drift. Need: store the asset hash
**and** the IIIF image API canonical URL + the specific derivative parameters, and define behavior
when a re-fetch hash-mismatches (re-quarantine downstream? notify consumer?).

**F. Metrics are mostly leading-indicator/process metrics dressed as outcomes.** "≥5,000 cleared
items," "≥70% cache hits," "100% manifest coverage" are pipeline-health metrics. Only one row
("downstream artifacts actually delivered to beneficiaries ≥1 project ships") is a true outcome, and
its target (**≥1** project shipping **≥1** artifact) is extremely weak for a 12-month horizon —
it lets the project declare partial success on a single delivered alt-text. There is no metric for
*beneficiary-side quality or acceptance* (e.g., transcriptions accepted back by By the People; alt-
text rated useful by a screen-reader user). The "outcomes, not vanity counts" philosophy is stated
but the table mostly counts plumbing.

**G. "By the People accepts contributed transcriptions back" is assumed, not verified — and it is
likely false as a direct API.** By the People / Concordia transcriptions are **human-volunteer
transcribed and human-volunteer reviewed**, then pushed back into loc.gov; there is **no documented
ingest path for externally machine-generated transcriptions** (https://crowd.loc.gov/about/). The
plan lists "contribute corrected transcriptions back upstream" as a beneficiary mechanism and a By
the People interaction, but Concordia's model would very likely **reject or distrust** bulk AI text.
This is a load-bearing assumption in the project's framing ("contributing back upstream") that the
open questions flag only weakly.

**H. No de-duplication against work already done.** Chronicling America already ships **METS/ALTO
OCR** for its newspapers; Internet Archive already has OCR for millions of books; Newspaper Navigator
already extracted 1.56M+ images with captions. The plan's fan-out could spend escrow/volunteer effort
re-OCRing or re-captioning material that is already transcribed. There is no "is this already done
upstream?" gate before fan-out — a real waste and arguably a "verified need" failure per Hee-Lee Oss.

**I. Smaller items:** (1) the proposal file `governance/proposals/loc-public-domain-engine.md`
**does not exist** (plan admits it leads the proposal) — a process gap. (2) "Owner: TBD" and
maintainer/all-reviewers TBD means **every** governance seat is empty; the plan is a spec without a
team. (3) The cultural-sensitivity screen is specified as a *detector* but TK Labels are applied **by
communities via the Local Contexts Hub**, not auto-detectable from LoC metadata
(https://localcontexts.org/labels/about-the-labels/) — so "check for TK Labels" will almost always
find none in LoC records, giving false comfort; the screen needs collection-level heuristics
(ethnographic/Indigenous collections) + human review, not a label lookup. (4) No explicit
licence-compatibility logic for **CC-BY-SA share-alike propagation** into downstream lanes that emit
CC0 — that is a real conflict the plan waves at but doesn't resolve.

---

## 2. Competitive landscape

No existing project does exactly this (a *conservative, auditable rights-gate + polite protocol as
reusable infra*). But many adjacent efforts overlap on pieces, and the project must position against
them.

**LoC "By the People" / Concordia** — LoC's own crowdsourced transcription platform; open-source
Concordia codebase; volunteers transcribe + other volunteers review; output goes back into loc.gov
and is released to the public domain as bulk datasets
(https://crowd.loc.gov/about/, https://github.com/LibraryOfCongress/concordia).
*Strengths:* official, trusted, in-the-loop with loc.gov, PD output, real community.
*Weaknesses/gaps:* human-only (no AI assist in the loop), no rights-gate-as-infra (LoC curates
campaigns by hand), no programmatic fan-out to other downstream uses (alt-text, translation), and
**no documented path to ingest external machine transcriptions**.

**Smithsonian Transcription Center** — pan-Smithsonian "volunpeers" transcribe + review; output
searchable across SI systems (https://transcription.si.edu/about). *Strengths:* mature community,
strong review discipline. *Weaknesses:* Smithsonian-only corpus, human-only, not LoC, not infra.

**Zooniverse** — world's largest people-powered research platform; sophisticated text-transcription
tooling (collaborative Transcription Task, ALICE aggregation/editor), increasingly AI-enhanced
(https://www.zooniverse.org/projects, https://help.zooniverse.org/transcription-project-guide/).
*Strengths:* scale, proven aggregation methods, project-builder for any institution.
*Weaknesses:* generic platform (you bring your own corpus + rights clearance), no LoC integration,
no rights-gate, AI is assistive not a fan-out engine.

**FromThePage** — hosted wiki-style transcription/indexing for GLAMs; imports from IIIF / CONTENTdm /
PDF, exports to many formats + API; multiple review configs
(https://fromthepage.com/, https://content.fromthepage.com/). *Strengths:* strong IIIF/GLAM ingest +
export, flexible review. *Weaknesses:* commercial SaaS, institution-driven, no rights determination,
no LoC-specific politeness layer.

**Transkribus** — leading AI HTR/OCR platform; 300+ public models, flagship Text Titan trained on
30M+ words, credit-based pricing (free 50 credits/mo; ~€15/mo+; 1 credit/handwritten page)
(https://www.transkribus.org/plans, https://help.transkribus.org/credit-system). *Strengths:*
best-in-class historical HTR, multilingual/multi-script, trainable models.
*Weaknesses:* paid/credit-metered, closed platform, no rights-gate, no PD-fan-out; it's an *engine* a
project like this could feed *into*, not a competitor to the gate.

**eScriptorium + Kraken** — open-source HTR platform (Kraken engine, PSL/Scripta); train/fine-tune
models in-browser, export structured data (https://escriptorium.eu/about/). *Strengths:* fully open,
no per-page cost, strong for complex scripts/manuscripts. *Weaknesses:* self-hosted/technical, no
rights logic, no LoC pipeline.

**Wikisource** — human-curated PD/open digital library; ProofreadPage shows scan beside text for
side-by-side proofreading; OCR (incl. Transkribus integration) seeded then human-verified; output
CC0/CC-BY/CC-BY-SA (https://en.wikipedia.org/wiki/Wikisource,
https://diff.wikimedia.org/2023/07/13/enabling-handwritten-text-recognition-on-wikisource-using-transkribus-ocr-engine/).
*Strengths:* huge volunteer base, rigorous human proofreading, ideal *downstream sink* for cleared
texts. *Weaknesses:* its own rights bar is conservative-but-manual, no programmatic intake of an
external "cleared-item" feed, no LoC etiquette layer.

**Internet Archive OCR (Tesseract)** — fully open OCR stack since ~2020; hOCR/chOCR word- and
character-level output for millions of books (https://archive.org/developers/ocr.html).
*Strengths:* massive scale, open output. *Weaknesses:* OCR quality "all over the map," "fast mode"
under load degrades quality and books aren't re-queued (https://archive.org/developers/ocr.html;
https://bibwild.wordpress.com/2023/07/18/) — i.e., a real *quality gap* a Claude-assisted correction
lane could fill.

**Newspaper Navigator (LoC Labs)** — ML pipeline that extracted 7 visual-content classes from 16.3M
Chronicling America pages (1.56M+ images w/ captions), open + PD
(https://news-navigator.labs.loc.gov/, https://arxiv.org/abs/2005.01583). *Strengths:* proves
LoC-blessed ML-on-PD, ready-made image corpus + captions. *Weaknesses:* one-off research artifact,
no rights-gate generalization, no alt-text/translation fan-out — *a perfect upstream input* to this
project.

**GLAM Workbench** — Tim Sherratt's open Jupyter notebooks/tools for GLAM data incl. LoC data jams
(https://glam-workbench.net/). *Strengths:* gold-standard "polite, reproducible GLAM data access"
patterns and harvesting recipes. *Weaknesses:* notebooks/recipes, not productized infra, AU/NZ focus,
no rights-gate-as-a-service. **Closest philosophical sibling** — worth aligning with, not competing.

**LoC "Free to Use and Reuse" sets** — 100+ curated themed sets LoC asserts are PD/no-known-
copyright/cleared (https://www.loc.gov/free-to-use/). *Strengths:* LoC pre-clearance, easy starting
corpus. *Weaknesses:* hedged language ("believes... no known copyright"), tiny curated subset, not an
API-native rights signal.

---

## 3. Gaps the competition leaves open (that we can fill)

1. **Rights-clearance as reusable, auditable infrastructure.** Every competitor either curates
   rights by hand (LoC, Smithsonian, Wikisource) or punts rights entirely to the user (Zooniverse,
   FromThePage, Transkribus, eScriptorium). **Nobody ships a deny-by-default, golden-tested, machine-
   checkable rights-gate + provenance manifest as a library others can adopt.** This is the genuine
   white space.
2. **Politeness-as-a-protocol against a known-fragile, key-less, adaptive-throttling API.** LoC's API
   blocks rather than meters and degrades under load (CAPTCHA-below-limits). No competitor packages a
   battle-tested, CAPTCHA-aware, AIMD-backoff LoC client. GLAM Workbench has recipes; nobody has a
   hardened library.
3. **A fan-out router that turns one cleared item into the *right* downstream task** (image→alt-text,
   text→translation/OCR-correction, AV→captions, tabular→dataset). All competitors are single-mode.
4. **AI-assisted quality on top of existing-but-poor OCR.** Internet Archive OCR is openly "all over
   the map"; Chronicling America METS/ALTO is raw. A *correction* lane (not re-OCR) is unfilled.
5. **Provenance/repro contract usable by the wider commons** (JSON-LD aligned to schema.org/Dublin
   Core/IIIF). Newspaper Navigator and By the People emit datasets, but no standardized *cleared-item
   contract* others can ingest.
6. **An ethics screen decoupled from copyright** (TK/Indigenous, human remains, living-person PII).
   None of the transcription platforms enforce "PD ≠ ethically clear" at the pipeline level.

---

## 4. Differentiators to win (concrete, defensible)

1. **The gate *is* the product, and it's auditable.** Deny-by-default + a public **quarantine ledger
   with reasons** + a **golden-test corpus with negative cases in CI** is a trust artifact no
   competitor offers. "Show me why you *didn't* clear that" is the defensible moat — it's how you
   earn LoC Labs / library trust where a heuristic crawler never would.
2. **Provenance you can replay.** Frozen API snapshot + rule-that-cleared-it + content hash + TTL +
   jurisdiction means any downstream artifact is reproducible and legally legible years later. This
   is what makes the feed *adoptable* by risk-averse institutions.
3. **Politeness as a credential, not a constraint.** A CAPTCHA-aware, adaptive, contact-identified
   client that *demonstrably* reduces LoC load (≥70% conditional-304 reuse) turns "yet another
   crawler" into "the good citizen LoC Labs points others to." Politeness is the partnership on-ramp.
4. **Agent-neutral, open, non-commercial infra (MIT code / CC0 outputs).** Transkribus is paid;
   FromThePage is SaaS. Being free, open, and explicitly non-profit aligns with GLAM values and lets
   Wikisource/IA/Wikimedia ingest outputs without licence friction.
5. **Network-effect spine.** One rights-gate feeds *many* Hee-Lee Oss lanes; each new downstream lane makes
   the shared gate more valuable. Competitors are vertically siloed; this is horizontal infra.
6. **Human-in-the-loop on rights by design** (the `needs-review` middle state + counsel-reviewed
   vocabulary). The defensible claim "no AI ever decides public-domain status here" is exactly what
   makes the AI-assisted *downstream* work palatable to institutions.

---

## 5. Claude API leverage

Where an Anthropic API key + Claude (multimodal vision, long context, tool use, batch + prompt
caching for cost control, structured/JSON output) measurably improves the product — run in the
**funded lane** (`packages/runner`) under a hard per-task budget cap:

**High-value uses (Claude assists, human/CI verifies):**
1. **OCR correction over existing text (highest ROI).** Don't re-OCR — *correct*. Feed Chronicling
   America METS/ALTO and Internet Archive hOCR (openly "all over the map") + the page image to a
   Claude vision model and have it produce a cleaned transcription with a confidence/uncertainty
   marker per low-confidence span. Fills the documented IA/CA quality gap directly.
2. **Alt-text drafting for cleared images** (feeds `a11y-alttext-commons`). Claude vision drafts
   descriptive alt-text + extended long-descriptions for PD photos/maps/posters; a human (ideally a
   screen-reader user) approves. Newspaper Navigator's 1.56M extracted images are a ready input.
3. **Translation drafting of cleared PD texts** (feeds `public-domain-translations`), with native-
   speaker review as the gate. Long context lets whole documents translate coherently.
4. **Transcription assist for print/typescript** (not a By the People replacement): first-pass
   transcription a human verifies; route handwriting to Transkribus/Kraken where stronger.
5. **Metadata enrichment & routing.** Claude classifies media type, detects language, suggests the
   right downstream lane, and proposes schema.org/Dublin Core fields for the cleared-item contract —
   structured JSON output validated against the JSON Schema.
6. **Cultural-sensitivity *triage* (flag, never clear).** Claude can *surface* candidate sensitive
   material (ethnographic, Indigenous, human-remains, possible living-person PII) for the human
   reviewer — raising recall on a screen that LoC metadata alone misses.
7. **Cost/throughput engineering:** Batch API for the non-interactive fan-out, prompt caching for the
   repeated rights-vocabulary/system context, and token-budget caps per task to honor escrow.

**Where Claude must NOT decide (hard line):**
- **Rights / public-domain determination.** The whole project's integrity rests on *affirmative,
  recorded, human/counsel-reviewed* clears. Claude may *parse* rights fields and *propose* a mapping
  candidate for the vocabulary table, but the `eligible` decision, the `needs-review` adjudication,
  and the counsel sign-off on `rights/vocabulary.yml` stay human. An LLM guess is exactly the
  "best-effort heuristic clear" the plan (correctly) forbids.
- **Final cultural-sensitivity / TK exclusion** and **living-person PII calls** — Claude flags;
  humans (with Indigenous-data competence where relevant) decide.
- **Date-based PD inference** — Claude must never *infer* a missing publication date to clear an
  item; if the metadata doesn't affirmatively state it, it's `ineligible`, full stop.
- **High-stakes downstream content** (medical/legal/safety) still requires that lane's credentialed
  expert sign-off + "not advice" label.

---

## 6. Ten concrete optimizations

1. **Make the politeness client CAPTCHA-aware.** Detect `text/html` / CAPTCHA bodies and treat them
   as a hard throttle signal (back off + circuit-break), never feed them to the JSON/rights parser.
   This is both a correctness fix and a politeness fix.
2. **Replace the static token bucket with adaptive concurrency (AIMD).** Since LoC limits float
   downward under load, additively grow concurrency on success, multiplicatively cut on 429/CAPTCHA;
   keep `loc-policy.yml` as the *ceiling*, not the operating point.
3. **Prefer bulk/derived corpora first, crawl last.** Wire Newspaper Navigator, Chronicling America
   bulk OCR, and "Free to Use and Reuse" sets as first-class inputs; per-item `?fo=json` crawling is
   the documented fallback. Cuts LoC load and skips already-done work.
4. **Add an "already transcribed/captioned upstream?" gate before fan-out** to avoid re-doing IA/CA
   OCR or Newspaper Navigator captions — turn those into *correction* tasks instead of new work.
5. **Split the wrong-clear metric into copyright vs non-copyright-rights** (publicity/privacy/moral)
   and give the auditor a written decision rule for each, so "zero wrong-clears" is falsifiable for
   `NoC-US`-style items.
6. **Compute the PD date threshold from `currentDate`** (95-year rolling) and split the date rule by
   material type (published vs unpublished vs sound recording vs foreign/URAA). Never hardcode a year.
7. **Hash and pin the *asset*, not just the JSON** — store IIIF canonical URL + derivative params +
   byte hash, and define re-fetch-mismatch behavior (re-quarantine + notify consumers).
8. **Ship a tiered counsel fallback** so M0 isn't hostage to securing a lawyer: adopt a published,
   conservative external baseline (DPLA/Europeana rights mappings) as a clearly-labeled interim
   ruleset, with counsel review as an upgrade, not a blocker.
9. **Add prompt caching + Batch API + per-task token caps** to every Claude-assisted lane; emit a
   public cost-per-cleared-item / cost-per-delivered-artifact figure (fits Hee-Lee Oss's funded-lane
   ledger ethos).
10. **Add a beneficiary-acceptance metric** (transcriptions accepted by a target sink such as
    Wikisource; alt-text rated useful by a screen-reader user) so success is measured at delivery,
    not at fan-out — and pilot the Wikisource ProofreadPage path as the realistic "contribute back"
    sink instead of assuming By the People ingest.

---

## 7. Parallel & perpendicular spin-offs

**Parallel (reuse the same spine on adjacent corpora):**
- **`rights-gate-core` as a standalone library** generalized beyond LoC: DPLA, Europeana, Internet
  Archive, Smithsonian Open Access, NARA. The gate + manifest + politeness pattern is corpus-agnostic
  — that's the real platform play.
- **A "polite GLAM client" package** (CAPTCHA-aware, conditional-request, AIMD) that GLAM Workbench-
  style users adopt directly — a community good in its own right.

**Perpendicular (downstream products built on the cleared feed):**
- **Cleared-item MCP server.** Expose the rights-cleared, provenance-stamped feed as an **MCP server**
  so *any* agent (Claude Desktop, IDEs, other Hee-Lee Oss lanes) can query "give me cleared PD images about
  X with manifests" — turning the gate into infrastructure other AI workflows pull from. High
  multiplier, low marginal cost.
- **A "PD provenance badge" / verification widget** institutions embed to show an item passed an
  auditable clear — trust-as-a-service.
- **Wikisource/Wikimedia Commons auto-ingest bridge** that pushes cleared + AI-corrected texts into
  ProofreadPage for human finishing — closes the "contribute back" loop realistically.
- **Open training-data sets** of high-quality, rights-clean, provenance-stamped image+alt-text and
  text+translation pairs (CC0) — directly useful to the open-ML commons, and a defensible "good deed"
  with measurable downstream reuse.
- **Accessibility-first reader** for cleared PD collections (alt-texted, screen-reader optimized) for
  blind/low-vision users — a visible beneficiary-facing product.

**Network effects:** each new downstream lane and each new corpus increases the value of the shared
gate; each MCP consumer increases reach; each contributed-back transcription increases LoC/Wikisource
goodwill (the partnership flywheel).

---

## 8. Open questions for the maintainer

1. **Counsel/rights reviewer:** who, and what is the *tiered* fallback so M0 can ship with a
   labeled interim ruleset rather than stalling indefinitely?
2. **"Contribute back upstream":** has anyone confirmed By the People / Concordia will accept
   externally machine-generated transcriptions? If not (likely), is Wikisource ProofreadPage the
   real sink — and should the plan say so?
3. **Non-copyright rights:** how will the audit handle `NoC-US` items that are copyright-clear but
   carry publicity/privacy/moral-rights risk (esp. for downstream translation reused abroad)?
4. **De-duplication:** will the engine check whether Chronicling America METS/ALTO, IA OCR, or
   Newspaper Navigator already did the work before fanning out a new task?
5. **Asset drift:** what happens when a re-fetched LoC asset hash no longer matches a clear that
   already produced a shipped downstream artifact?
6. **Date rule:** confirm the rolling 95-year computation and per-material-type sub-rules
   (unpublished, foreign/URAA, sound recordings) — and remove the hardcoded "1929."
7. **TK/cultural screen:** given TK Labels are community-applied via Local Contexts and rarely
   present in LoC metadata, what collection-level heuristics + human review replace a label lookup?
8. **First committed consumer/steward:** which Hee-Lee Oss lane (alt-text? translation?) commits to consume
   the feed at M2, and what is the LoC Labs engagement status?
9. **Funded-lane economics:** what is the target cost-per-delivered-artifact, and the hard per-task
   `fundedBudgetUsd` cap for the Claude-assisted lanes?
10. **Share-alike:** how is CC-BY-SA source propagation reconciled with CC0-emitting downstream lanes?

---

### Key sources
- LoC By the People / Concordia: https://crowd.loc.gov/about/ · https://github.com/LibraryOfCongress/concordia
- Smithsonian Transcription Center: https://transcription.si.edu/about
- Zooniverse: https://www.zooniverse.org/projects · https://help.zooniverse.org/transcription-project-guide/
- FromThePage: https://fromthepage.com/ · https://content.fromthepage.com/
- Transkribus: https://www.transkribus.org/plans · https://help.transkribus.org/credit-system
- eScriptorium/Kraken: https://escriptorium.eu/about/
- Wikisource: https://en.wikipedia.org/wiki/Wikisource · https://diff.wikimedia.org/2023/07/13/enabling-handwritten-text-recognition-on-wikisource-using-transkribus-ocr-engine/
- Internet Archive OCR: https://archive.org/developers/ocr.html · https://bibwild.wordpress.com/2023/07/18/investigating-ocr-and-text-pdfs-from-digital-collections/
- Newspaper Navigator: https://news-navigator.labs.loc.gov/ · https://arxiv.org/abs/2005.01583
- GLAM Workbench: https://glam-workbench.net/
- LoC API limits: https://www.loc.gov/apis/json-and-yaml/working-within-limits/ · https://guides.loc.gov/chronicling-america/additional-features
- LoC Free to Use & Reuse: https://www.loc.gov/free-to-use/ · https://www.loc.gov/legal/understanding-copyright/
- rightsstatements.org NoC-US: https://rightsstatements.org/page/NoC-US/1.0/
- Local Contexts / TK Labels: https://localcontexts.org/labels/about-the-labels/
