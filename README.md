# scRNA-seq Hypoxia Classification

Can we tell from a single cell's gene expression whether it was grown in **hypoxia** (low oxygen) or **normoxia**, and does that prediction carry over to other cell lines and sequencing technologies?

This repository contains our final report notebook for the **AI Lab in the Mathematical Modelling in Machine Learning** course at Bocconi University the spring semester of 2026. We analyse single-cell RNA-seq data from two breast-cancer cell lines (**MCF7** and **HCC1806**), each profiled with two technologies (**SmartSeq** and **DropSeq**). The pipeline covers quality control and EDA, dimensionality reduction, clustering, supervised classification, cross-dataset transfer and a multi-dataset "universal" hypoxia classifier.

> **Note:** The datasets were provided by the course and are **not included** in this repository. See [Data](#data) below.

## Notebook outline

1. Introduction, materials and methods
2. Data loading and inventory: labels, class balance, train/test compatibility
3. Quality control: unfiltered vs filtered SmartSeq data
4. Distributional EDA: scale, `log2(x + 1)` decision, sparsity, duplicate genes
5. Dimensionality reduction per dataset: PCA, UMAP, Kernel PCA, Factor Analysis, PLS-DA, ICA, Sparse PCA, random projections
6. Clustering per dataset: k-means, KNN-graph, hierarchical, DBSCAN
7. Supervised classification within each dataset: logistic regression, linear SVM, random forest, PCA + LR, Gaussian NB, with leakage-safe CV pipelines
8. Cross-dataset transfer learning: transfer matrix, asymmetry, statistical tests
9. Feature stability and consensus hypoxia biomarkers
10. Multi-dataset vs single-dataset training
11. Universal hypoxia classifier: leave-one-cell-line-out, leave-one-technology-out, bootstrap CIs
12. Final test-set prediction
13. Conclusion

## Key findings

- Hypoxia is **highly predictable within a single dataset** (same cell line and technology).
- Performance **drops when transferring across cell lines or sequencing technologies**. Both biological and technical variation shape what the models learn.
- A **universal classifier trained on all four datasets** does not match the best within-dataset models. It still gives meaningful predictions on every dataset, so it trades some accuracy for generality.

See Section 17 of the notebook for the full discussion.

## Data

The notebook expects the course data files in two folders next to the notebook:

```
.
├── AI_Lab_Report.ipynb
├── SmartSeq/
│   ├── HCC1806_SmartS_MetaData.tsv
│   ├── HCC1806_SmartS_Unfiltered_Data.txt
│   ├── HCC1806_SmartS_Filtered_Data.txt
│   ├── HCC1806_SmartS_Filtered_Normalised_3000_Data_train.txt
│   ├── HCC1806_SmartS_Filtered_Normalised_3000_Data_test_anonim.txt
│   └── MCF7_SmartS_...                       (same five files for MCF7)
└── DropSeq/
    ├── HCC1806_Filtered_Normalised_3000_Data_train.txt
    ├── HCC1806_Filtered_Normalised_3000_Data_test_anonim.txt
    ├── MCF7_Filtered_Normalised_3000_Data_train.txt
    └── MCF7_Filtered_Normalised_3000_Data_test_anonim.txt
```

## Running the notebook

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate    macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

Then open `AI_Lab_Report.ipynb` in Jupyter or VS Code, select the environment as the kernel and run all cells.

You don't need the data just to *read* the report: all outputs and figures are saved in the notebook.

## Authors

- Oliver Dahle
- Rassul Jakupov
- Senghun Baik
- Andrey Mukhin

## License

The code and written content are released under the [MIT License](LICENSE). The datasets are not covered by this license and are not distributed here.
