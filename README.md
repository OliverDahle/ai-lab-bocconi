# scRNA-seq Hypoxia Classification

Can we tell from a single cell's gene expression whether it was grown in **hypoxia** (low oxygen) or **normoxia**, and does that prediction carry over to other cell lines and sequencing technologies?

This repository contains our final report notebook for the **AI Lab in the Mathematical Modelling in Machine Learning** course at Bocconi University in the spring semester of 2026. We analyse single-cell RNA-seq data from two breast-cancer cell lines (**MCF7** and **HCC1806**), each profiled with two technologies (**SmartSeq** and **DropSeq**). The pipeline covers quality control and EDA, dimensionality reduction, clustering, supervised classification, cross-dataset transfer and a multi-dataset "universal" hypoxia classifier.

> **Note:** The datasets were provided by the course and are **not included** in this repository. See [Data](#data) below.

## Notebook outline

Section numbers match the notebook.

- **0–2** Setup, introduction, materials and methods
- **3–5** Data loading, quality control and EDA: labels, class balance, unfiltered vs filtered SmartSeq, `log2(x + 1)` decision
- **6–9** Dimensionality reduction: PCA, UMAP, Kernel PCA, Factor Analysis, PLS-DA, ICA, Sparse PCA, random projections
- **10** Clustering: k-means, KNN-graph, hierarchical, DBSCAN
- **11** Supervised classification within each dataset: linear, tree-ensemble, PCA-based and baseline models in leakage-safe CV pipelines
- **12** Cross-dataset transfer learning
- **13** Feature stability and consensus hypoxia biomarkers
- **14** Multi-dataset vs single-dataset training
- **15** Universal hypoxia classifier: leave-one-cell-line-out, leave-one-technology-out, bootstrap CI
- **16** Final test-set prediction
- **17** Conclusion

## Key findings

- **Within a single dataset, hypoxia is almost perfectly predictable**: cross-validated ROC-AUC of 0.99–1.00 on all four datasets.
- **Performance drops across cell lines and technologies.** Transfer works best when the two datasets share many of their 3,000 selected genes.
- **The universal classifier does not generalise to unseen settings.** Trained on the 70 genes shared by all four datasets, it reaches ROC-AUC 0.89 on unseen MCF7 cells but 0.62 on unseen HCC1806 cells, and is no better than chance (0.44–0.48) on an unseen sequencing technology.

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
