# MAGIC Gamma Event Classifier

Classify telescope events as gamma or hadron using measured shower characteristics. The observations are Monte Carlo simulations.

## Dataset

[UCI MAGIC Gamma Telescope dataset](https://archive.ics.uci.edu/dataset/159/magic%2Bgamma%2Btelescope) (dataset ID 159), 19,020 records. The source is public and is fetched by the runner; the raw dataset is not committed.

## Run

```bash
python -m pip install -r requirements.txt
python main.py --output-dir artifacts
```

The runner saves metrics, holdout predictions, and a reusable model in the ignored output directory. The public [`reports/benchmark.json`](reports/benchmark.json) contains aggregate results only; no row-level records are published.

## Holdout results

A stratified random 75/25 split (seed 42) is used. Numeric inputs are median-imputed; the random-forest classifier uses 400 trees and balanced subsampling.

| Accuracy | Balanced accuracy | Macro F1 | Weighted F1 | Majority baseline accuracy |
|---:|---:|---:|---:|---:|
| 0.881 | 0.859 | 0.867 | 0.880 | 0.648 |

ROC-AUC: **0.937**.

Full aggregate metrics and the exact split seed are in [`reports/benchmark.json`](reports/benchmark.json).

## Limits

This dataset contains Monte Carlo-simulated telescope events, not live telescope observations. A random split does not demonstrate deployment or instrument-shift performance. These are one-time benchmark results, not service-level, production, or causal claims.

## Reproducibility

The model and split use seed 42. Re-running downloads source data from UCI and regenerates local artifacts. Model binaries, raw inputs, and row-level predictions are excluded from this public repository.
