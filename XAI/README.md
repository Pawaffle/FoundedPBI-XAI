# XAI Project 

This folder contains the explainability-oriented part of the FoundedPBI project, developed during a 6-month exchange at [HEIG-VD](https://heig-vd.ch) (CI4CB laboratory, January–July 2026) as part of a Metropolia Engineering School exchange program.

The goal of this exploratory work was to investigate what SHAP-based methods can reveal about a genomic foundation model ensemble, while documenting their strengths, limitations, and practical challenges. The methods are functional, but their results are sensitive to the choice of baseline and should therefore be treated as diagnostics rather than ground truth. The report discusses the limitations of each approach in detail. If something breaks — and it might — the most likely causes and potential solutions are documented in documentation/ under "Possible modifications and issues."

**In Short:** Hierarchy SHAP (Nb2) is the most robust method in the current setup. Simple mean ablation (Nb1) is fast and easy to use, but highly sensitive to the choice of baseline. And DNABERT-2 does something odd during misclassifications — worth looking into.

For the reasoning behind the chosen methods, interpretation of the results, and practical recommendations, the [`final report`](./documentation/Report_PBI_XAI.pdf) is the primary reference.


## What is FoundedPBI?

FoundedPBI is a modular ensemble of three genomic foundation models — Nucleotide Transformer v2 (NT2), DNABERT-2, and MegaDNA — that predicts phage–bacterium interaction (PBI) from raw DNA sequences. Each model produces an embedding; the six embeddings (one per model per organism) are concatenated, compressed by PCA to 500 components, and passed to a neural classifier.

This XAI layer sits on top of that classifier and asks: which of the three models actually contributed most to each prediction?

---


## Project structure (need to add main and utils/parser_xai)
```
XAI/
├── documentation/
├── bundle/
└── jupiter/
  ├── annex/
  └── earlyCheckpoints/ 
```
- [`documentation/`](./documentation/)
Contains the final report as PDF and the notebook usage manual. Start here if you are new to explainability part of the project.

- [`bundle/`](./bundle/) 
Contains the trained model, two PCA objects (phage and bacteria), the test dataset, compressed embedding data, and the main configuration file. This is everything the notebooks need to run.

- [`jupiter/`](./jupiter/)
Main notebook workspace. Contains the three explanation notebooks (Nb1–Nb3), a utility notebook for restoring the dataset, supporting annex material, and earlier development checkpoints.

- [`annex/`](./jupiter/annex/)
Supporting outputs and side experiments accompanying the notebooks and the report. Includes exported local/global explanation examples and the PCA attribution study (Annex B in the report).

- [`earlyCheckpoints/`](./jupiter/earlyCheckpoints/)
Earlier versions and intermediate milestones, kept for development traceability. Not part of the main workflow, but useful if you want to understand how the implementation evolved.

---

## Integration with FoundedPBI

The notebooks are designed to run from the **project root directory** of the FoundedPBI repository. They use a dedicated configuration parser (`pbi_utils/config_parser_XAI.py`) instead of the original one — this avoids loading all three foundation models into VRAM when they are not needed (the notebooks work on pre-computed embeddings, not raw sequences).

The `bundle/` folder provides a self-contained set of artifacts so the notebooks can run without re-training. If you want to feed freshly trained artifacts instead, see the integration guide in `documentation/`.


## Related work

This project is a direct predecessor to an upcoming Bachelor's thesis at Metropolia / HEIG-VD focused on cross-attention-based PBI prediction with built-in interpretability. The XAI pipeline developed here informed the direction of that work.

**Original FoundedPBI repository:** [CI4CB-lab/FoundedPBI-code](https://github.com/CI4CB-lab/FoundedPBI-code)
