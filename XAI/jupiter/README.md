# Jupiter

This folder contains the main notebook workspace for the XAI exploration. It includes the three core explanation notebooks, a utility notebook for loading the dataset, supporting annex material, and earlier development checkpoints kept for traceability.

In the report, these notebooks correspond to the **Model Importance** section #2 (Nb1–Nb3).

## Main notebooks (to be polished)

- [`restore_compress_emb.ipynb`](./restore_compress_emb.ipynb)  
  Start here. This utility notebook restores and verifies the compressed embedding data and dataset objects stored in `bundle/`.

- [`nb1_kernel_explainer.ipynb`](./nb1_kernel_explainer.ipynb) — Mean ablation  
  Implements block-level KernelSHAP with a 6-dimensional binary mask over the six embedding blocks (NT2, DNABERT-2, MegaDNA × phage/bacteria). Also includes a 3-dimensional "frozen-side" variant that holds one organism fixed while perturbing the other. 
  
  **When to use:** fast local analyses, sanity checks, and baseline comparison experiments. Results are highly sensitive to the choice of baseline: read Section 2.1.3 of the report before interpreting outputs.

- [`nb2_two_level_hierarchy.ipynb`](./nb2_two_level_hierarchy.ipynb) — Hierarchy SHAP  
  Implements `shap.PartitionExplainer` with a two-level coalition tree that respects the phage/bacteria split. Redistributes block-level attributions from the full embedding space. Includes global confusion-matrix analysis (TP/TN/FP/FN breakdowns).

  **When to use:** global diagnostics and any analysis where you want a more robust, baseline-stable result. This is the most reliable method in the current toolset. `RANDOM_SEED = 48` was used for all reproducible runs.

- [`nb3_independent_explainer.ipynb`](./nb3_independent_explainer.ipynb) — Per-base perturbation (draft)  
  An attempt at a more "by the book" SHAP analysis operating directly on the full ~18k-dimensional embedding space. Computationally expensive and not adopted into the main workflow, it kept as a documented exploration. Described in the report as "Clear per-base perturbation (Nb3)" and explicitly marked as not recommended for routine use.

## Supporting folders

- [`annex/`](./annex/) - Supporting outputs and side experiments accompanying the notebooks and the report.


- [`earlyCheckpoints/`](./earlyCheckpoints/) - Earlier versions and intermediate milestones, kept for development traceability.

<br>

### Note: 
*All explanations are baseline-dependent. The final interpretation should always be done with that in mind — the report covers this in detail.*