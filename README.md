# Depth over Fidelity in Fixed-Budget Noisy ES

This is a **standalone reproducibility package** for the ICML 2026 paper:
*"Depth over Fidelity in Fixed-Budget Noisy Evolution Strategies"*

It includes:
- Python implementation of **Residual Bootstrapping (RB-PEM)** and **Probe-and-Switch**
- Experiment runners and analysis scripts
- Precomputed artifacts under `evidence/` (all paper figures and tables)
- One-command end-to-end reproduction

## Algorithm Naming

The paper uses the following names:

| Paper Name | Code Name | Description |
|------------|-----------|-------------|
| **Residual Bootstrapping** | `BERW-Hetero` | Selection-stage uncertainty integration |
| **Probe-and-Switch** | `ProbeSwitch-MR(t=0.12)` | Adaptive method selection |
| CMA-ES | `CMA-ES-sep` | Baseline |
| Resample (k=N) | `CMA-ES-Resample(k=N)` | Evaluation-stage resampling |
| UH-CMA-ES | `UH-CMA-ES(maxevals=30)` | Uncertainty-handling baseline |

See `docs/ALGORITHMS.md` for the complete mapping.

## Quickstart

### 1) Create environment and install dependencies

```bash
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -U pip
pip install -r requirements.txt
pip install -e .
```

### 2) Install COCO (optional, required for BBOB experiments)

```bash
pip install cocoex
```

See `docs/INSTALL.md` for troubleshooting.

### 3) Verify precomputed results

```bash
python3 tools/verify_evidence.py
```

### 4) Reproduce all experiments

```bash
python3 tools/reproduce_all.py --workers 4
```

Options:
- `--quick`: fast sanity check (small subset)
- `--skip-existing`: resume interrupted runs
- `--suite coco|probes|external|diagnostics`: run specific suite

## Directory Layout

```
├── src/             # Python modules (algorithms, baselines, utils)
├── tools/           # Experiment runners and plotting scripts
├── evidence/        # Precomputed results (paper figures/tables)
├── docs/            # Documentation
│   ├── ALGORITHMS.md   # Code name ↔ paper name mapping
│   ├── EXPERIMENTS.md  # Claim → experiment → command
│   ├── FIGURES.md      # Figure guide with data sources
│   ├── INSTALL.md      # Installation instructions
│   └── OUTPUTS.md      # Output directory conventions
└── Results/         # Raw outputs (generated, gitignored)
```

## Key Evidence Files

| Paper Element | Location |
|---------------|----------|
| Figure 1 (Money Plot) | `evidence/paper_figures/figure1_money_plot.pdf` |
| Figure 2 (Depth-Fidelity) | `evidence/paper_figures/figure2_depth_fidelity_bubble.pdf` |
| Figure 3 (Ranking) | `evidence/paper_figures/figure3a_ranking.pdf` |
| Figure 4 (Rank by Probe) | `evidence/paper_figures/figure_rank_by_probe.pdf` |
| Figure 5 (Single-Crossing) | `evidence/paper_figures/figure3b_single_crossing.pdf` |
| Figure 6 (Transfer) | `evidence/paper_figures/figure3c_transfer.pdf` |
| Table 1 | `evidence/paper_tables/table_probeswitch_comparison.tex` |
| Appendix A1-A11 | `evidence/paper_figures/Appendix/` |

## Notes

- This repository ships with precomputed `evidence/` for immediate inspection
- A full rerun overwrites `evidence/` in-place
- All experiments use fixed random seeds for reproducibility
