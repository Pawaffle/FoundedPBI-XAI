# Annex

Supporting materials that accompany the main notebooks and the final report. Provided for transparency, reproducibility, and to give future readers something concrete to look at without re-running everything.

---

## Contents

### (A) [Local and Global Explanation Outputs (Exploration Tests)](./Local%20and%20Global%20Explanation%20Outputs%20(Exploration%20Tests).pdf)
Exported explanation results from the exploration phase, including local (per-pair) and global (confusion-matrix) SHAP attribution examples. The final conclusions in the report are based on these results. If you want to re-evaluate the work with fresh eyes — or look for something that was missed the first time — this is a good place to start.

### (B) [`pca_shap_testing.ipynb`](./pca_shap_testing.ipynb) — PCA attribution study (Annex B)
A proof-of-concept notebook exploring whether SHAP attributions could be extended to the PCA component level — that is, asking not just "which model contributed?" but "which PCA dimensions within that model contributed?". This corresponds to **Annex B** in the final report.

Some output cells are blank due to export issues, so the notebook is partial. It is kept as an idea for future exploration rather than a finished result.

<br>

### Note

*Any findings and conclusions should be taken from the main report, not from these materials directly. Think of this folder as the raw evidence behind the report's claims — useful for verification and as a jumping-off point for follow-up work.*