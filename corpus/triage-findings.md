# Phase 4 triage run findings

- Queue size (phase-4 residue): 31955
- Triaged this run: 198
- Verified: 138
- Needs human review: 62
- Claim/content mismatches: 24
- Skipped (already triaged on a prior run): 3593
- Routed to human, oversized (not line-reviewable): 2
- Routed to human, too large for the model: 0
- Routed to human, triage error: 0
- **Untriaged remaining (budget did not cover): 28162**

### Drafted categories

- bugfix: 94
- packaging: 50
- documentation: 21
- feature: 15
- security: 13
- unknown: 5

### Cost & cache

- Input tokens: 200092 (cache read 0, cache write 449104)
- Output tokens: 141956
- Cache-hit ratio: 0.0%
- Cost (backend-reported): $6.0816
- Cost (estimated at API rates for claude-sonnet-4-6): $5.4242
- Per triaged patch (estimated): $0.0274

### Candidate deterministic rules (for human approval, never auto-applied)

_No sound cluster: none reached the threshold with a structural key unique to one category._

### Refused by the counterexample gate (structure does not determine category)

- types={code};shape=code-only spans 7 categories (bugfix 1793, packaging 278, security 270, feature 185, documentation 149, unknown 8, test 3): NOT a rule -- structure does not determine category.
- types={data};shape=mixed spans 6 categories (packaging 621, bugfix 317, documentation 121, feature 72, security 28, unknown 2): NOT a rule -- structure does not determine category.
- types={build,code};shape=mixed spans 5 categories (packaging 98, bugfix 36, feature 31, documentation 3, security 3): NOT a rule -- structure does not determine category.
- types={code,test};shape=mixed spans 5 categories (bugfix 82, security 35, packaging 31, feature 14, documentation 1): NOT a rule -- structure does not determine category.
- types={code,data};shape=mixed spans 6 categories (bugfix 51, packaging 50, feature 33, security 15, documentation 8, unknown 1): NOT a rule -- structure does not determine category.
- types={code,doc};shape=mixed spans 6 categories (feature 33, documentation 27, bugfix 6, security 4, packaging 3, unknown 1): NOT a rule -- structure does not determine category.
- types={test};shape=mixed spans 4 categories (bugfix 39, packaging 25, security 1, test 1): NOT a rule -- structure does not determine category.
- types={data,test};shape=mixed spans 5 categories (bugfix 17, packaging 17, feature 8, documentation 1, security 1): NOT a rule -- structure does not determine category.
- types={build,code,data};shape=mixed spans 4 categories (feature 18, bugfix 7, packaging 6, security 2): NOT a rule -- structure does not determine category.
- types={build,test};shape=mixed spans 3 categories (packaging 24, bugfix 3, feature 2): NOT a rule -- structure does not determine category.
- types={data,doc};shape=mixed spans 5 categories (documentation 16, feature 6, bugfix 2, packaging 2, security 2): NOT a rule -- structure does not determine category.
- types={code,data,doc};shape=mixed spans 5 categories (documentation 8, packaging 7, feature 4, security 2, bugfix 1): NOT a rule -- structure does not determine category.
- types={build,doc};shape=mixed spans 2 categories (documentation 12, packaging 8): NOT a rule -- structure does not determine category.
- types={build,code,doc};shape=mixed spans 3 categories (feature 6, packaging 5, bugfix 4): NOT a rule -- structure does not determine category.
- types={code,data,test};shape=mixed spans 5 categories (security 5, packaging 4, feature 2, bugfix 1, documentation 1): NOT a rule -- structure does not determine category.
- types={build,code,test};shape=mixed spans 3 categories (packaging 9, bugfix 2, documentation 1): NOT a rule -- structure does not determine category.
- types={build,code,data,doc};shape=mixed spans 4 categories (feature 4, bugfix 1, packaging 1, security 1): NOT a rule -- structure does not determine category.
- types={code,doc,test};shape=mixed spans 4 categories (documentation 3, security 2, bugfix 1, packaging 1): NOT a rule -- structure does not determine category.
- types={build,code,data,test};shape=mixed spans 2 categories (packaging 4, feature 3): NOT a rule -- structure does not determine category.
- types={build,data,doc};shape=mixed spans 4 categories (packaging 3, bugfix 1, documentation 1, feature 1): NOT a rule -- structure does not determine category.
- types={code,data,doc,test};shape=mixed spans 3 categories (packaging 3, bugfix 1, unknown 1): NOT a rule -- structure does not determine category.
- types={build,data,test};shape=mixed spans 2 categories (packaging 3, feature 1): NOT a rule -- structure does not determine category.
