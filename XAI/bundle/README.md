# Bundle

This folder contains the essential files required to work with the delivered XAI notebooks without re-training the model or regenerating embeddings.


## Contents

| File | Description |
|---|---|
| `best_model_XAI.yaml` | Main configuration file for the XAI setup. Passed to `config_parser_XAI` on notebook startup. |
| `config_parser_XAI` | Alternative configuration object, that evoids heavy model loading and stores unique to this fork information |
| `trained_model.pth` | Saved weights of the FoundedPBI classifier used in this study. |
| `pca_phage.pkl` | Fitted PCA object for the phage-side embeddings (reduces to 500 components). |
| `pca_bacteria.pkl` | Fitted PCA object for the bacteria-side embeddings (reduces to 500 components). |
| `compressedEmbData.pt` | Pre-computed PCA-compressed meta-embeddings for the test set. Used directly by the notebooks to avoid recomputing embeddings at runtime. |
| `test_dataset.pt` | Serialized test dataset (phage–bacterium pairs with labels). |
| | |

## How this connects to the pipeline

The notebooks load these files via `config_parser_XAI`, which has the paths hardcoded to point at this folder:

```python
self.model_path = os.path.join("XAI/bundle/trained_model.pth")
self.bacteria_pca_path = os.path.join("XAI/bundle/pca_bacteria.pkl")
self.phage_pca_path = os.path.join("XAI/bundle/pca_phage.pkl")
self.test_path = os.path.join("XAI/bundle/test_dataset.pt")
```

This means you don't need to run the full training pipeline to use the notebooks — just make sure all files above are present and `config_parser_XAI` located under the `project_root/pbi_utils/` folder.

---

## Re-generating the bundle from a fresh training run

If you have run the original `main.py` pipeline with the project-side modifications described in the report (Section 2.3.4), the training output folder will contain a freshly trained model, new PCA objects, and a new test dataset. You can replace the files here with those outputs, or update the paths in `config_parser_XAI` to point at the output folder directly.

Key things to watch out for when re-generating:
- **PCA auto-save** must be enabled in `main.py` (lines ~308–330). Not present in the original codebase — see the report for the exact change.
- **Test-set saving** is currently a draft implementation. The split happens before oversampling, which can cause data leakage if oversampling was applied earlier. Worth fixing before using for any serious evaluation.


## Notes

- Files are tightly coupled to the notebook workflow in `jupiter/`.
- The `compressedEmbData.pt` file is the output of the embedding compression step — regenerating it requires access to the original raw embeddings (`.h5` files), which are not stored here due to size.
- For additional context on what each artifact represents, see Section 2.3 of the final report.