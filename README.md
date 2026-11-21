# consilience-benchmarks

Public benchmarks and studies for the checks in the [Consilience engine](https://github.com/Anuja-Khatri/consilience-core). Each one has:
- a protocol committed before any run;
- labels or targets taken from cited sources;
- an independent second-way checker that imports nothing from the engine;
- receipts that `consilience verify` re-checks.

Limits come first in every results file.

| Folder | Engine check | What it asks | Status |
|---|---|---|---|
| [`evaluator-stress/`](evaluator-stress/) | `consilience stress` | Does a scoring function used for program search (AlphaEvolve, OpenEvolve, ShinkaEvolve, CodeEvolve, reinforcement learning) accept invalid answers, trust self-reported values, or break invariances, before an optimiser exploits it? | **Done** (45 of 111 contracts run): [results](evaluator-stress/results/RESULTS.md) |
| [`pooling-2026/`](pooling-2026/) | `consilience compare-table` (bioactivity pack) | Which ChEMBL potency records may be pooled, and do the poolable ones agree? | **Incomplete** (data source failed; no results) |

## evaluator-stress in brief

**Contracts:** 89 public scoring functions from five collections, plus 22 pre-fix and post-fix versions of 13 publicly reported scorer bugs. The five collections:
- Google DeepMind's AlphaEvolve problem and results repositories;
- OpenEvolve;
- CodeEvolve;
- ShinkaEvolve;
- Google Cloud's AlphaEvolve samples.

**Results of the 45-contract run:**

| Measure | Result |
|---|---|
| Known bugs caught | 11 of 13 |
| Fixed versions still flagged for their bug | 1 of 11 (a real remaining defect) |
| New findings in a 21-contract random sample | 3, mostly invalid input; none in the self-report or invariance classes |
| Independent second way | 76 of 76 findings agree |
| Fresh clone | All 47 receipts verify; pinned re-runs reproduce their receipt hashes |
| Runtime | Median 16 s per scorer |

**What it is:** a useful pre-run checker for common classes of scorer loopholes. **What it is not:** a discovery engine for deep ones.

```bash
git clone https://github.com/Anuja-Khatri/consilience-benchmarks && cd consilience-benchmarks
pip install -r evaluator-stress/requirements.txt          # consilience 0.3.0 from PyPI + the scorers' own dependencies
consilience verify evaluator-stress/results/receipts/DM/flat_polynomials_c_minus/receipt.json
consilience stress evaluator-stress/contracts/LABELS/oe548_cpr_pre/contract.yaml \
  --steps-from evaluator-stress/results/receipts/LABELS/oe548_cpr_pre/receipt.json --out /tmp/rerun   # re-run one contract
```

A walk-through notebook is in `evaluator-stress/examples/stress_demo.ipynb`. The protocol, deviations and every number are in `evaluator-stress/PREREGISTRATION.md`, `VERIFICATION_LOG.md` and `results/RESULTS.md`.

## Provenance

This repository was split out of consilience-core on 21 Nov 2026, with history preserved, so that the engine repository holds only the engine. Commit hashes changed in the split. The preregistration timestamps can still be checked in consilience-core, where the original commits remain:

| Event | consilience-core | here |
|---|---|---|
| evaluator-stress preregistration final, before any run | 6049a69 | 29c3f5f |
| pooling-2026 preregistration, before any analysis run | bc61d0b | 4dae439 |

Files written before the split (the preregistrations, some logs) still name paths such as `benchmarks/evaluator-stress/` from the old layout. They are left unedited so that they match their timestamped commits.

## Licence and claims

MIT, except vendored third-party code and published constructions, which keep their licences (`NOTICE.md`). Every statement about a third-party scorer concerns **the published code at the stated commit** only, not its authors' internal systems or published results.
