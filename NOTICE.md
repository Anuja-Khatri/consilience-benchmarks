# Third-party material in this repository

Everything here is MIT (see `LICENSE`) except the vendored scoring code and published constructions, which keep their own licences.

| Folder | Source | Licence |
|---|---|---|
| `evaluator-stress/contracts/DM/`, `evaluator-stress/pilot/dm_*` | google-deepmind/alphaevolve_repository_of_problems @ 8f44745 | Code Apache-2.0; other material (published constructions) CC BY 4.0, attributed to Google DeepMind |
| `evaluator-stress/contracts/DMR/` | google-deepmind/alphaevolve_results @ 4226acb | Code Apache-2.0; other material CC BY 4.0 |
| `evaluator-stress/contracts/OE/`, `evaluator-stress/pilot/oe_*` | algorithmicsuperintelligence/openevolve @ ac5f8f5 | Apache-2.0 |
| `evaluator-stress/contracts/CE/` | inter-co/science-codeevolve @ a43fd88 | Apache-2.0 |
| `evaluator-stress/contracts/SH/` | SakanaAI/ShinkaEvolve @ 1bf7113 | Apache-2.0 |
| `evaluator-stress/contracts/G/` | Google-Cloud-AI/alphaevolve-on-googlecloud @ 019a2d2 | Apache-2.0 |
| `evaluator-stress/contracts/LABELS/` | the pre-fix and post-fix commits listed in `evaluator-stress/SOURCES.yaml` | as the source repository above |

- **File headers:** every vendored file starts with a header naming its repository, commit and path. Code below that header is unmodified, except that imports were added where only scoring cells were copied from a notebook.
- **Folder notices:** per-folder `NOTICE.md` files give details.
- **Licence text:** the Apache-2.0 text is at https://www.apache.org/licenses/LICENSE-2.0.
- **No downloaded data:** no ChEMBL data and no non-commercial data are committed. The pooling study downloads ChEMBL data locally (CC BY-SA 3.0).
- **Scope of claims:** every statement about these files concerns the published code at the stated commit only. It says nothing about the authors' internal systems or published results.
