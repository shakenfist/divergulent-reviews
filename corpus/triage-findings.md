# Phase 4 triage run findings

- Queue size (phase-4 residue): 29754
- Triaged this run: 100
- Verified: 57
- Needs human review: 43
- Claim/content mismatches: 19
- Skipped (already triaged on a prior run): 4470
- Routed to human, injection-suspect (never sent to the LLM): 0
- Routed to human, oversized (not line-reviewable): 0
- Unlocked by residue (generated mark): 0
- Routed to human, too large for the model: 0
- Routed to human, triage error: 0
- **Untriaged remaining (budget did not cover): 25184**

### Drafted categories

- packaging: 35
- bugfix: 34
- documentation: 13
- security: 10
- feature: 6
- unknown: 2

### Cost & cache

- Input tokens: 99447 (cache read 0, cache write 161589)
- Output tokens: 63786
- Cache-hit ratio: 0.0%
- Cost (backend-reported): $2.5151
- Cost (estimated at API rates for claude-sonnet-4-6): $2.2247
- Per triaged patch (estimated): $0.0222

### Candidate deterministic rules (for human approval, never auto-applied)

_No sound cluster: none reached the threshold with a structural key unique to one category._

### Refused by the counterexample gate (structure does not determine category)

- types={code};shape=code-only spans 7 categories (bugfix 2398, packaging 364, security 333, feature 249, documentation 190, unknown 20, test 3): NOT a rule -- structure does not determine category.
- types={data};shape=mixed spans 6 categories (packaging 781, bugfix 416, documentation 149, feature 98, security 39, unknown 2): NOT a rule -- structure does not determine category.
- types={build,code};shape=mixed spans 5 categories (packaging 126, bugfix 50, feature 40, security 7, documentation 3): NOT a rule -- structure does not determine category.
- types={code,data};shape=mixed spans 6 categories (bugfix 69, packaging 63, feature 45, security 18, documentation 12, unknown 1): NOT a rule -- structure does not determine category.
- types={code,test};shape=mixed spans 5 categories (bugfix 101, security 41, packaging 37, feature 16, documentation 2): NOT a rule -- structure does not determine category.
- types={code,doc};shape=mixed spans 6 categories (feature 44, documentation 38, bugfix 11, packaging 6, security 5, unknown 1): NOT a rule -- structure does not determine category.
- types={test};shape=mixed spans 4 categories (bugfix 39, packaging 25, security 1, test 1): NOT a rule -- structure does not determine category.
- types={data,test};shape=mixed spans 5 categories (packaging 21, bugfix 20, feature 10, documentation 1, security 1): NOT a rule -- structure does not determine category.
- types={build,code,data};shape=mixed spans 4 categories (feature 23, packaging 15, bugfix 8, security 2): NOT a rule -- structure does not determine category.
- types={data,doc};shape=mixed spans 5 categories (documentation 23, feature 7, bugfix 5, packaging 2, security 2): NOT a rule -- structure does not determine category.
- types={build,test};shape=mixed spans 3 categories (packaging 32, bugfix 4, feature 2): NOT a rule -- structure does not determine category.
- types={code,data,doc};shape=mixed spans 5 categories (documentation 12, feature 7, packaging 7, bugfix 2, security 2): NOT a rule -- structure does not determine category.
- types={build,doc};shape=mixed spans 3 categories (documentation 12, packaging 10, bugfix 1): NOT a rule -- structure does not determine category.
- types={code,data,test};shape=mixed spans 5 categories (packaging 7, security 7, feature 3, bugfix 2, documentation 1): NOT a rule -- structure does not determine category.
- types={build,code,test};shape=mixed spans 3 categories (packaging 15, bugfix 2, documentation 1): NOT a rule -- structure does not determine category.
- types={build,code,doc};shape=mixed spans 4 categories (feature 8, packaging 5, bugfix 4, documentation 1): NOT a rule -- structure does not determine category.
- types={build,code,data,doc};shape=mixed spans 4 categories (feature 6, bugfix 2, packaging 1, security 1): NOT a rule -- structure does not determine category.
- types={code,doc,test};shape=mixed spans 5 categories (documentation 3, security 3, feature 2, bugfix 1, packaging 1): NOT a rule -- structure does not determine category.
- types={build,code,data,test};shape=mixed spans 2 categories (packaging 6, feature 3): NOT a rule -- structure does not determine category.
- types={build,data,doc};shape=mixed spans 4 categories (packaging 5, bugfix 1, documentation 1, feature 1): NOT a rule -- structure does not determine category.
- types={build,data,test};shape=mixed spans 2 categories (packaging 5, feature 1): NOT a rule -- structure does not determine category.
- types={code,data,doc,test};shape=mixed spans 4 categories (packaging 3, bugfix 1, documentation 1, unknown 1): NOT a rule -- structure does not determine category.
