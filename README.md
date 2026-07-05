# divergulent-reviews

The **source of truth** for the [divergulent](https://github.com/shakenfist/divergulent)
patch classification: the append-only ledger of verdicts (deterministic rules, a
verified LLM triage tier, and signed human review) plus the review axes
(security-risk, install-base *reach*, reviewability).

This repository holds the ledger under version control as **`ledger/`** — a
canonical, byte-deterministic export of the ledger sqlite. That export is what CI
consumes to build and publish the signed classification bundle clients download.
Committing it (rather than the sqlite) means:

- the diff of each commit is a **reviewable** "here are the verdicts I just added"
  — the human-in-the-loop publish gate;
- the irreproducible human + LLM review work is **durably backed up** by this
  repository's remote (the working `ledger.sqlite` lives on scratch storage);
- CI can **reach** it (GitHub Actions cannot read a local scratch disk).

The export is a *directory* of compact JSONL, not one file: the two big
append-only tables (`decision`, `observation`) are **sharded by calendar month**,
so no single file grows toward GitHub's 100 MB per-file limit as the append-only
ledger accumulates. New work appends to the current month's shard.

## Layout

```
.divergulent          # data-root marker (divergulent-classify discovers the root here)
ledger/               # THE tracked artifact: the sharded ledger export (source of truth)
  manifest.json       #   {export_schema, shards, rows}
  decision-YYYY-MM.jsonl     #   decisions, sharded by month
  observation-YYYY-MM.jsonl  #   observations (risk/reach/reviewability), sharded by month
  rule.jsonl, note.jsonl, review_queue.jsonl, meta.jsonl   #   small tables, whole
corpus/               # the working corpus (gitignored except the notes below)
  bodies/             #   content-addressed patch bodies        (regenerable)
  ledger.sqlite       #   the live ledger you mutate as you review (regenerable from ledger/)
  fingerprints.sqlite #   the fingerprint index                 (regenerable)
  popcon.sqlite       #   the reach-axis install-base snapshot   (regenerable)
  findings.md,        #   your analysis notes                    (tracked)
  triage-findings.md
cache/                # client-style published cache dir (gitignored)
venv/                 # python virtualenv (gitignored; recreate, never move)
```

Everything except the `ledger/` export and the `*.md` notes is regenerable and
gitignored. The `ledger.sqlite` is rebuilt from the export with
`divergulent-classify import ledger`; the corpus is rebuilt from the Debian
archive.

## A review session

All curation verbs run through `divergulent-classify` from inside this data
root (the `.divergulent` marker anchors discovery, so no paths are typed).

```bash
# 1. Orient. One screen: the un-settled residue, verdicts by category, the
#    security-risk breakdown (and how many elevated+ patches are still
#    unreviewed), the pending human-review queue, whether a `record` run is
#    due, and the published-cache age.
divergulent-classify status

# 2. Freshen the published cache if status flags it stale (> 14 days).
#    Data-consuming verbs nag about a stale cache too (suppress with --no-pull).
divergulent cache pull

# 3. Decide whether to re-pull popcon (the reach-axis install-base input).
#    Check the pinned snapshot's date:
sqlite3 corpus/popcon.sqlite "select value from popcon_meta where key='snapshot_date'"
#    Reach is anchor-relative, so popcon only needs a slow cadence -- roughly
#    monthly, or when returning after a long gap. After a re-pull, re-run
#    `record` so reach observations are recomputed against the new snapshot.
divergulent-classify popcon

# 4. Deterministic tier. Re-applies the current rules to the ledger --
#    idempotent and non-destructive (LLM/human decisions are preserved), so it
#    is always safe. Run it when status says a record run is due (a rule was
#    bumped/added, or an axis has coverage gaps) or after a popcon refresh.
divergulent-classify record

# 5. LLM tiers, riskiest-first. `risk` scores security risk (a prioritisation
#    signal, not a verdict) so triage and human review reach the scariest
#    patches first; `triage` categorises the substantive residue. Both default
#    to the local `claude` CLI backend (billed to the operator's subscription).
divergulent-classify risk --limit 50
divergulent-classify triage --limit 50

# 6. Human review -- the top of the verdict precedence, recorded as a
#    Sigstore-signed ManualDecision. Either front-end writes byte-identical
#    verdicts; `requeue` sends a fingerprint back for another look and
#    `history` shows recent decisions.
divergulent-classify review          # interactive CLI, next highest-priority item
divergulent-classify web             # local web UI on 127.0.0.1
```

Occasionally a freshly pulled cache brings **new package versions** whose
patches are not in the corpus yet. Growing the corpus is a separate, slower
pass -- crawl the new bundle, then re-fingerprint and re-record:

```bash
python -m divergulent.classify.corpus <bundle> corpus/
python -m divergulent.classify.measure corpus/
divergulent-classify record
```

Analysis notes go in `corpus/findings.md` / `corpus/triage-findings.md` (the
tracked notes files). When the session is done, export and commit -- see below.

## The publish loop

```bash
# after a review session:
divergulent-classify export            # ledger.sqlite -> ledger/ (sharded, canonical)
git add ledger && git diff --cached    # review "the verdicts I just added"
git commit && git push                 # the human-in-the-loop publish gate

# then run divergulent's build-classification workflow (workflow_dispatch,
# publish: true), which checks out this repo, imports ledger/, builds the lean
# signed bundle, and uploads it to the rolling 'classification' release.
```

See `docs/plans/PLAN-patch-classification-phase-05-bundle.md` in the divergulent
repository for the full design.
