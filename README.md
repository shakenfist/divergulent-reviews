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
