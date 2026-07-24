# Quarantine Ledger — Documentation

**Project:** loc-public-domain-engine  
**Component:** Quarantine Ledger (M1 Output)  
**Output License:** CC0-1.0  
**Version:** 1.0.0

## Overview

The quarantine ledger is an **append-only, version-controlled log** documenting every item not cleared by the loc-public-domain-engine's rights-gate. It demonstrates the gate's conservatism and allows external observers to audit gate decisions.

The gate operates on a **deny-by-default** principle: only items with affirmative, recorded rights determinations are eligible for fan-out; everything ambiguous or uncertain is quarantined with a reason.

## Files in This Directory

| File | Purpose |
|------|---------|
| `quarantine.jsonl` | Append-only ledger; one JSON record per line, one per non-cleared item |
| `quarantine-summary.json` | Machine-readable aggregate counts by exclusion reason |
| `QUARANTINE-SUMMARY.md` | Human-readable summary table and interpretation |
| `QUARANTINE-SCHEMA.json` | JSON Schema defining the record format (use for validation) |
| `README.md` | This file |

## Quick Start: Parsing the Ledger

### Reading the JSONL File

The `quarantine.jsonl` file is line-delimited JSON (JSONL): each line is a complete, valid JSON object representing one quarantined item.

**Python example:**

```python
import json

with open("quarantine.jsonl") as f:
    for line in f:
        record = json.loads(line)
        print(f"{record['locId']} — {record['reason']}: {record['reasonMessage']}")
```

**Node.js example:**

```javascript
const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
  input: fs.createReadStream('quarantine.jsonl')
});

rl.on('line', (line) => {
  const record = JSON.parse(line);
  console.log(`${record.locId} — ${record.reason}: ${record.reasonMessage}`);
});
```

### Validating Records

All records in the ledger conform to `QUARANTINE-SCHEMA.json`. To validate:

**Using `ajv-cli` (Node.js):**

```bash
npx ajv validate -s QUARANTINE-SCHEMA.json -d quarantine.jsonl --invalid=log
```

**Using Python `jsonschema`:**

```python
import json
import jsonschema

schema = json.load(open("QUARANTINE-SCHEMA.json"))
with open("quarantine.jsonl") as f:
    for i, line in enumerate(f, 1):
        record = json.loads(line)
        try:
            jsonschema.validate(record, schema)
        except jsonschema.ValidationError as e:
            print(f"Line {i} invalid: {e.message}")
```

## Record Format

Each record in the ledger contains:

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `locId` | string | Library of Congress item identifier (unique within LoC) |
| `reason` | string | Exclusion category: `restricted`, `undetermined`, `needs-review`, or `sensitive-hold` |
| `reasonMessage` | string | Human-readable explanation of the exclusion |
| `collection` | string | LoC collection/source name (e.g., "Chronicling America") |
| `timestamp` | string (ISO 8601) | When the item was evaluated (UTC) |
| `jurisdiction` | string | Rights jurisdiction: `US` (default), `US-state`, or `international` |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `metadata` | object | LoC rights fields and context (see below) |
| `reviewer_note` | string | Note added by a rights/cultural reviewer during re-evaluation |

### Metadata Subfields

The optional `metadata` object may contain LoC fields that informed the exclusion:

- `rights` — LoC "rights" field (e.g., a rightsstatements.org URI)
- `access_restricted` — Boolean; whether LoC marked the item as access-restricted
- `collection_rights` — Collection-level rights determination, if present
- `item_rights` — Item-level rights determination (overrides collection)
- `date` — Publication/creation date (may include uncertainty markers like "[circa 1906]" or "1905-1925 (uncertain)")
- `derivative_status` — Assessment of whether the item is a derivative work
- `sensitivity_flag` — If `reason` is `sensitive-hold`, a code indicating the type of sensitivity (e.g., `ethnographic-content`, `indigenous-content`, `personal-information`)
- `collection_identifier` — Collection name/identifier in LoC's system

## Exclusion Reasons Explained

### `undetermined`

**What it means:** LoC's metadata does not affirmatively establish the item's rights status.

**Gate policy:** Deny by default. An item is eligible only with an affirmative, recorded rights determination; absence of rights information means the item is ineligible.

**Example scenarios:**
- LoC rights field is empty or generic ("rights unknown")
- LoC rights field points to `http://rightsstatements.org/vocab/UND/1.0/` (rightsstatements.org "Undetermined")
- Rights metadata is missing or unrecognizable

**Next steps:**
- LoC may update the item's metadata with clearer rights information
- A qualified rights reviewer may adjudicate the item if additional external sources are available
- The item will remain quarantined until an affirmative determination is made

### `restricted`

**What it means:** LoC metadata explicitly restricts access or indicates copyright/other legal restrictions.

**Gate policy:** Absolutely ineligible. No amount of additional review overrides an explicit restriction.

**Example scenarios:**
- `access_restricted: true` in LoC metadata
- Rights field indicates ongoing copyright
- Access restrictions due to donor agreement or institutional policy

**Next steps:**
- Only LoC can remove the restriction in their source metadata
- The item cannot be fanned out regardless of other circumstances

### `needs-review`

**What it means:** The item presents a borderline case that requires expert rights-reviewer adjudication.

**Gate policy:** Held in an expert-review queue; not auto-fanned until a qualified reviewer makes an explicit determination.

**Example scenarios:**
- Publication date is ambiguous or non-standard ("circa 1906", "1905-1925 (uncertain)") — pre-1929 PD-by-date status cannot be confirmed without clarification
- Collection-level rights differ from item-level rights (both must align)
- Derivative work status is unclear (e.g., LoC's digitization of a PD original, but copyrighted restoration/metadata)
- Rights field references a category or jurisdiction that requires domain expertise to interpret

**Next steps:**
- A qualified rights reviewer (or counsel) manually examines the item
- Reviewer determines whether the item qualifies for `eligible` or should remain `ineligible` / `quarantined`
- Result is recorded, and the item is either cleared or moved to a permanent exclusion

### `sensitive-hold`

**What it means:** The item passes the rights-gate (or is otherwise eligible) but is flagged by the cultural-sensitivity / privacy screen.

**Gate policy:** Held pending review by ethics/cultural authorities. Public domain ≠ ethically clear.

**Example scenarios:**
- Material contains Indigenous/Traditional-Knowledge content (marked with TK Labels in metadata)
- Ethnographic or anthropological material about specific communities
- Content relating to human remains
- Historical records surfacing potential personal information about living or recently deceased individuals
- Material requiring community consultation before reuse

**Next steps:**
- Flagged item is queued for review by a cultural authority or ethics reviewer
- Reviewer may: (a) clear the item for fan-out with appropriate attribution/context, (b) exclude it permanently, or (c) forward to the relevant community for consultation
- Result is recorded, and the item's status is updated

## Aggregate Counts

A summary of quarantine counts is published in two formats:

### `quarantine-summary.json`

Machine-readable summary showing:
- Total quarantined items
- Count and percentage for each reason
- Interpretation notes on gate conservatism

### `QUARANTINE-SUMMARY.md`

Human-readable table format with explanations.

**Key insight:** The distribution of exclusion reasons demonstrates the gate's philosophy:

- **High "undetermined" %**: The gate treats ambiguity conservatively (denies by default).
- **Restricted items are immovable**: Once LoC restricts an item, it stays excluded.
- **Significant "needs-review" %**: Edge cases and borderline determinations get expert attention, not heuristic resolution.
- **Cultural sensitivity is separate**: Even PD items may be flagged for ethical review.

## Append-Only & Auditable

The quarantine ledger is **append-only**: records are never deleted or modified in place. This enables:

1. **Auditability**: A complete history of exclusion decisions
2. **Re-evaluation tracking**: If an item is re-run in a future pipeline stage and receives a different determination, a new record is appended (the old record remains for history)
3. **Version control**: The entire ledger is committed to Git, with commit messages documenting the pipeline run (date, source collection, number of items processed)

### Git History Example

```bash
git log --oneline ledger/quarantine.jsonl
# 1a2b3c Publish M1 quarantine ledger: Chronicling America (30 quarantined items)
```

## Maintenance & Updates

### Per-Run Workflow

Each pipeline run appends new records to the ledger:

1. Pipeline processes items from an approved LoC source
2. Non-cleared items are logged with reason codes
3. Ledger is appended to (not rewritten)
4. Changes are committed to Git with a descriptive message
5. Maintainer reviews new entries before publication

### Re-evaluation

If LoC updates metadata for a previously quarantined item:

- The item may be re-run through the gate
- If it now qualifies, a new `eligible` record is created (not in the quarantine ledger)
- If it remains ineligible, a new quarantine record is appended with the new determination + the original reason for reference

## External Consumer Guidelines

### For Rights Reviewers

- Use the `needs-review` section of the ledger to identify items requiring adjudication
- Check `metadata.date` and `metadata.derivative_status` to inform pre-1929 PD-by-date decisions
- Record your determination (cleared or remain quarantined) in the cleared-items manifest or in an updated quarantine record

### For Cultural / Ethics Reviewers

- Use the `sensitive-hold` section to identify flagged items
- `metadata.sensitivity_flag` indicates the category (e.g., `indigenous-content`, `ethnographic-content`)
- Consult appropriate communities or authorities per your institution's policy
- Record clearance or exclusion decision

### For Data Consumers

- Use `quarantine-summary.json` to understand the gate's selectivity and reasoning
- Do NOT assume that quarantined items are forbidden; they are simply not cleared for automated fan-out
- Quarantined items may later be eligible if LoC updates metadata or an expert determines otherwise
- Always refer back to LoC's authoritative source for current metadata and any restrictions

### For Tool Builders

- Parse the ledger using the JSONL format (one record per line)
- Validate records against `QUARANTINE-SCHEMA.json`
- Use `timestamp` to identify newly-added records since your last sync
- Use `locId` to deduplicate if you process the ledger multiple times
- Aggregate counts using `reason` for transparency dashboards or reports

## Support & Feedback

For questions, corrections, or updates to the ledger format:

- **Project:** loc-public-domain-engine (Hee-Lee Oss)
- **License:** CC0-1.0 (public domain for metadata and records)
- **Repository:** See PLAN.md and TASKS.md for project documentation
- **Contact:** Refer to the project's maintainer or point of contact

---

**Last Updated:** 2026-07-23  
**Format Version:** 1.0.0  
**Output License:** CC0-1.0
