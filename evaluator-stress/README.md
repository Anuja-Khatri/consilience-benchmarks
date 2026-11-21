# evaluator-stress: a benchmark for checking scoring code before program search

The benchmark behind `consilience stress` (engine guide: [`docs/stress.md`](https://github.com/Anuja-Khatri/consilience-core/blob/main/docs/stress.md) in consilience-core).

| Path | What it is |
|---|---|
| `results/RESULTS.md` | **Start here.** Results of the 45-contract run, limits first |
| `PREREGISTRATION.md`, `LABELS.yaml`, `SELECTION_45.txt` | Protocol, the 13 labelled bugs, and the seeded sample, all committed before any run |
| `SOURCES.yaml`, `CONTRACTS.sha256` | Pinned source commits and the frozen contract hashes |
| `contracts/{DM,DMR,OE,CE,SH,G,LABELS}/` | One folder per scorer: `contract.yaml`, glue, reference and the vendored scorer. `COVERAGE*.md` lists what was in and out of scope |
| `pilot/` | The 10 pre-lock pilot cases; `tests/test_pilot_a1.py` checks they still give the same verdicts |
| `run_benchmark.py`, `check_independent.py`, `validate_contract.py` | The runner, the independent second-way checker (imports nothing from the engine), and a contract validator |
| `CONTRACT_AUTHORING.md` | How the contracts were written |
| `VERIFICATION_LOG.md` | Every deviation, fix and re-check |
| `results/receipts/`, `results/extra/` | Every receipt, with stored counterexamples |
| `examples/stress_demo.ipynb` | A walk-through of four real cases |

**Running it:**

```bash
pip install -r evaluator-stress/requirements.txt
consilience verify evaluator-stress/results/receipts/LABELS/oe548_cpr_pre/receipt.json
CONSILIENCE_SLOW=1 python -m pytest -q evaluator-stress/tests            # the pilot acceptance test, a few minutes
```

**Warning:** `run_benchmark.py` re-runs contracts and **overwrites** the stored receipts and results files. To re-run one contract without touching them, use `consilience stress ... --steps-from <stored receipt> --out <elsewhere>`.
