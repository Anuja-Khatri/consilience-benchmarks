# pooling-2026: which bioactivity records may be pooled?

A preregistered study of `consilience compare-table` with the `bioactivity` pack. The question: when potency values (IC50, Ki, Kd, EC50) from ChEMBL are pooled for one target, how many pairs of records are comparable, and do the comparable ones agree?

**Status: incomplete. There are no results to quote.**
- **First full run void:** the ChEMBL web API returned damaged pages under load (80 pages with blank assay and target fields). The first run's numbers are void (`VERIFICATION_LOG.md`).
- **Fix:** the fetch and join scripts now refuse such pages.
- **Second run never finished:** the API then failed for hours, and the study was parked.
- **What is here:** the protocol, the scripts and the notebook, so anyone can run the study.

| File | What it is |
|---|---|
| `PREREGISTRATION.md` | The protocol, committed before any analysis run (consilience-core bc61d0b, here 4dae439) |
| `targets.json` | EGFR plus the 29 MoleculeACE targets, fixed before any run |
| `fetch.py`, `join.py` | Download activity records (sliced by year) and join assay fields. Data stays local and is never committed |
| `run_study.py`, `check_independent.py`, `write_results.py`, `make_figures.py` | The analysis, an independent second way, and the write-up |
| `package_dataset.py` | Packages a derived dataset (CC BY-SA 3.0, as ChEMBL) |
| `examples/egfr_pooling.ipynb` | Walk-through on EGFR (CHEMBL203), the example used in a public ChEMBL agent skill |
| `plugin/LIVE_RUN.md` | A recorded live run of the `consilience-pooling` agent plugin after that skill fetched records |

```bash
pip install -r pooling-2026/requirements.txt
python pooling-2026/fetch.py && python pooling-2026/join.py && python pooling-2026/run_study.py
```

The engine and the `bioactivity` pack are documented in consilience-core: `docs/compare-table.md` and `docs/packs/bioactivity.md`.
