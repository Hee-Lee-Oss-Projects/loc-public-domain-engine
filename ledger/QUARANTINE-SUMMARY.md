# Quarantine Ledger Summary — M1 Data Run

**Source:** Chronicling America (first approved high-PD source for M1)  
**Run Date:** 2026-07-23  
**Ledger File:** `ledger/quarantine.jsonl`  
**License:** CC0-1.0

## Exclusion Counts by Reason

| Reason | Count | Percentage | Description |
|--------|-------|-----------|-------------|
| **undetermined** | 12 | 40% | Rights determination is undetermined per LoC metadata |
| **restricted** | 7 | 23% | Access is restricted or copyrighted |
| **needs-review** | 6 | 20% | Borderline cases requiring expert rights review |
| **sensitive-hold** | 5 | 17% | Flagged by cultural-sensitivity/privacy screen |
| **TOTAL QUARANTINED** | 30 | 100% | All non-cleared items |

## Gate Transparency

This quarantine ledger demonstrates the rights-gate's conservative posture:

- **40% undetermined:** Items where LoC metadata does not affirmatively establish rights status; per the deny-by-default principle, all are withheld pending clarification or expert determination.
- **27% restricted:** Items explicitly marked with access restrictions or copyright; excluded per policy.
- **20% expert review:** Borderline cases (publication date formatting issues, collection/item-level conflicts, derivative work status ambiguity) held for qualified rights reviewer adjudication.
- **13% sensitivity flagged:** Items passing rights determination but flagged by the cultural-sensitivity screen (Indigenous/Traditional-Knowledge content, ethnographic material, potential personal information); held pending ethics/cultural authority review.

## Audit Trail

Every exclusion is recorded with:
- **locId:** The Library of Congress item identifier
- **reason:** A category from the defined exclusion taxonomy
- **reasonMessage:** A human-readable explanation
- **collection:** Source collection (e.g., Chronicling America)
- **timestamp:** When the item was evaluated
- **jurisdiction:** Rights jurisdiction (default: US)
- **metadata:** The LoC rights fields and collection context that prompted the exclusion

This structure allows:
- External observers to audit the gate's decisions
- Downstream review queues to action items by reason (e.g., rights reviewers prioritize `needs-review`, cultural reviewers prioritize `sensitive-hold`)
- Historical tracking if item metadata is updated (append-only ledger; items may be re-evaluated in future runs)

## File Format

See [`QUARANTINE-SCHEMA.json`](./QUARANTINE-SCHEMA.json) for the JSON Schema that validates the quarantine ledger.
