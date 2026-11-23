# One-Hour-Ahead Photovoltaic Power Forecasting

This repository preserves an earlier machine-learning study of one-hour-ahead photovoltaic (PV) power forecasting. It contains exploratory multilayer-perceptron notebooks, two CSV datasets, and the original presentation and project archive.

## Files

| File | Purpose |
| --- | --- |
| `(Multilayer Perceptron)  MLP.ipynb` | MLP experiment using `dataset1.csv` |
| `(Multilayer Perceptron) MLP+extension.ipynb` | Feature-extension workflow; writes `dataset1ApresExtension.csv` |
| `(Multilayer Perceptron)  MLP-Dataset1Extension.ipynb` | MLP experiment using the extended CSV |
| `dataset1.csv` | Original tabular input |
| `dataset1ApresExtension.csv` | Extended tabular input |
| `Presentation Of Project.pdf`, `Readme.pdf` | Original project materials |
| `Project-All Machine Learning Regression-1h-PVPrediction.z01`–`.z05` and `.zip` | Multipart project archive; keep all parts together |

## Run the notebooks

The notebooks use relative CSV paths and should be opened with the repository root as the working directory. Install the libraries used by the notebooks:

```bash
python -m pip install numpy pandas scikit-learn matplotlib seaborn jupyterlab
jupyter lab
```

Run the baseline notebook with `dataset1.csv`. To regenerate the extended input, run `MLP+extension.ipynb` first, then run `MLP-Dataset1Extension.ipynb`. The extended CSV is already present, so preserve a copy if you want to compare it with regenerated output.

## Scope and reproducibility

These are legacy exploratory notebooks, not a packaged training pipeline. They contain historical outputs and should be reviewed before treating their reported metrics as comparable results. In particular, verify the target definition, chronological split strategy, and preprocessing before using the experiments as a benchmark. No separate automated test suite or pinned environment is currently provided.

### Known temporal-evaluation limitations

The two MLP experiment notebooks use `train_test_split` with its default shuffling, so observations from later times can appear in the training data while earlier times appear in the holdout. Their `cross_validate(..., cv=5)` calls also operate on the full `X, y`, rather than a separate development-only time series. These historical outputs should not be treated as an unbiased one-hour-ahead forecast benchmark.

For a new experiment, preserve the timestamp, establish the target horizon and feature availability explicitly, split chronologically before fitting any learned preprocessing or selecting models, and reserve the last period for a single final evaluation. The original notebooks and archived results remain unchanged; this notice is not an implementation or validation of a replacement pipeline.
