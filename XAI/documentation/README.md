# Documentation

- [**Final report (PDF)**](XAI\documentation\Report_PBI_XAI.pdf) — The main reference for this project. Covers the biological and engineering context, a taxonomy of the implemented SHAP methods, implementation details, a friendly notebook usage guide, and conclusions with directions for future work. Read this first.

<br>

## Notebook usage — quick reference of section 2.3 in the report

All notebooks are configured through **Section 1 (Configuration)** at the top of each notebook. Under standard conditions, nothing else needs to be changed. The key variables are:

| Variable | What it controls |
|---|---|
| `PAIR_ID` | Index of the phage–bacterium pair to explain (local analysis) |
| `BASELINE_MODE` | Which baseline strategy to use (e.g. `'zero'`, `'mean'`, `'random_sample'`, `'decoupled'`, `'search_by_id'`) |
| `RANDOM_SEED` | Fixed seed for reproducibility (use `48` to match the results in the report) |
| `N_EVALS` | Number of perturbation evaluations (higher = slower but more accurate, mainly relevant for Nb2) |
| | |


## Integration with the original FoundedPBI pipeline

The notebooks depend on `pbi_utils/config_parser_XAI.py`, a dedicated parser that belongs to be alongside the original `config_parser`. Its purpose is to load only what the XAI notebooks actually need — the trained classifier, the two PCA objects, and the test dataset — without pulling the full set of foundation models into memory.

**To use the notebooks with the bundled artifacts** (default): no changes needed. The paths in `config_parser_XAI` are already hardcoded to point at `XAI/bundle/`.

**To use freshly trained artifacts**, the original `main.py` requires three small modifications (approximate line numbers given as navigation aid only — they may shift as the codebase evolves):

| Change | Location | Notes |
|---|---|---|
| PCA auto-save | `main.py` ~lines 308–330 | Add `pickle.dump(...)` for both phage and bacteria PCA objects. Not in the original codebase. |
| Test-set saving | `main.py` ~lines 932–943 | Add `torch.save(test, config.test_path)`. Currently a draft — watch for data leakage if oversampling was applied before the split. |
| Model saving | `main.py` ~lines 984–987 | Save trained model to `config.model_path`. |
| | |

After these changes, also copy the path definitions from `config_parser_XAI` into the original `config_parser`, pointing at the training output directory instead of `bundle/`. See Section 2.3.3 of the report for the exact lines.



## Known limitations and things that might break

- **Section 3 of NB (Data & Model Loading)** in each notebook assumes the config class modifications above have already been made. If they haven't, the test dataset and PCA objects need to be loaded manually — the fallback code is at the beginning of that section.
- **Section 2 of NB (Block definitions)** must be updated manually if the model configuration changes (e.g. a foundation model is added or removed, or the order in the config file changes).
- **Section 4 of NB (Baseline & Dataset)** may need adjustment if new baseline strategies are added or preprocessing changes. The current implementation uses a long `if` chain on `BASELINE_MODE` — a future improvement would be to replace it with an Enum.
- Notebooks must be run from the **project root directory**, not from within `XAI/`. But there is dedicated intro section for that in each of them.