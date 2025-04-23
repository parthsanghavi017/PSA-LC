# Identifying Diagnostic Markers and Therapeutic Targets for Psoriatic Arthropathy and Long Covid

## Objective
To identify shared diagnostic markers and therapeutic targets common to Psoriatic Arthropathy (PsA) and Long Covid by the means of bioinformatics and machine learning, focusing on shared immune and inflammatory pathways to inform clinical management and drug development towards treatment and control of future disease X.

## Introduction
Psoriatic Arthropathy (PsA) is an autoimmune condition characterized by chronic joint and skin inflammation, driven by cytokines like IL-17 and TNF-α. Long Covid, a post-infectious syndrome following SARS-CoV-2 infection, presents persistent symptoms such as fatigue and joint pain, linked to immune dysregulation and chronic inflammation. Both conditions share features of immune overactivity, cytokine-driven inflammation, and potential autoimmunity, making them ideal candidates for comparative analysis. This project adapts a bioinformatics and machine learning framework, to explore shared molecular mechanisms, diagnostic biomarkers, and therapeutic targets for PsA and Long Covid, aiming to enhance understanding and treatment of these complex diseases.

## Methods

### 1. Data Acquisition
Four datasets will be sourced from the Gene Expression Omnibus (GEO) database:
- **PsA Datasets**:
  - GSE130073: Includes synovial tissue samples from 20 PsA patients and 15 healthy controls (HC).
  - GSE95065: Comprises peripheral blood mononuclear cell (PBMC) samples from 30 PsA patients and 25 HC for external validation.
- **Long Covid Datasets**:
  - GSE163211: Includes PBMC samples from 25 Long Covid patients and 20 HC.
  - GSE171110: Comprises blood samples from 40 Long Covid patients and 30 HC for external validation.
Details of the datasets, including sample sizes and tissue types, will be summarized in a table.

<Pending>

### 2. Identification of Differentially Expressed Genes (DEGs)
The “limma” R package will be used to identify DEGs in GSE130073 (PsA) and GSE163211 (Long Covid) by comparing patient samples to HC. DEGs will be selected based on criteria of |log2 FC| ≥ 1 and adjusted p-value < 0.05. Volcano plots and heatmaps, generated using the “ggplot2” package, will visualize DEGs, highlighting the top 25 genes for each condition.

### 3. Weighted Gene Co-expression Network Analysis (WGCNA)
WGCNA will be applied to identify co-expressed gene modules associated with PsA and Long Covid. The top 25% of genes with the highest variance will be selected. The `goodSamplesGenes` function will filter out ineligible genes and samples, and a scale-free network will be constructed using the `pickSoftThreshold` function to determine optimal soft power β. Dynamic tree-cutting will identify gene modules, which will be correlated with clinical traits (e.g., joint inflammation in PsA, fatigue in Long Covid). Overlapping genes between PsA and Long Covid modules and DEGs will be visualized using a Venn diagram on a bioinformatics platform.

### 4. Functional Enrichment Analysis
Gene Set Enrichment Analysis (GSEA) will be performed using the “clusterProfiler” package (version 4.8.2) to identify enriched KEGG pathways in PsA and Long Covid. Additionally, GO and KEGG enrichment analyses will be conducted on the Metascape platform to elucidate biological roles of co-expressed genes, with a significance threshold of p < 0.01. Results will be visualized using Sankey dot pathway enrichment diagrams.

### 5. Construction of Protein-Protein Interaction (PPI) Network and Hub Gene Identification
PPI networks for shared genes will be constructed using the STRING platform, with an interaction score threshold > 0.4. Networks will be visualized in Cytoscape, and the cytoHubba plugin will identify hub genes based on maximal clique centrality measures, highlighting highly connected nodes critical to disease mechanisms.

### 6. Machine Learning for Screening Key Genes and Validation
Machine learning will be employed to identify and validate key genes:
- **LASSO Regression**: To perform LASSO logistic regression on GSE130073 and GSE163211 to select predictive genes, using the smallest lambda value for optimal disease prediction.
- **Support Vector Machine-Recursive Feature Elimination (SVM-RFE)**: SVM-RFE will iteratively eliminate less informative genes based on five-fold cross-validation to identify critical genes.
- **Validation**: Identified genes will be validated using independent datasets (GSE95065 for PsA, GSE171110 for Long Covid). Receiver Operating Characteristic (ROC) curves, generated with the “pROC” package, will assess diagnostic accuracy. Nomographs and calibration curves, constructed using the “rms” package, will evaluate predictive capability. Box plots, created with “ggplot2”, will visualize expression levels of diagnostic genes, with statistical significance denoted as *p < 0.05 and **p < 0.01.

### 7. Immune Infiltration Analysis
Yet to explore

## Application of Machine Learning
Machine learning plays a pivotal role in this study by enabling the identification of key genes with diagnostic and therapeutic potential. **LASSO regression** efficiently selects a sparse set of predictive genes by penalizing less relevant features, ensuring robust biomarker identification from high-dimensional gene expression data. **SVM-RFE** complements this by iteratively refining the gene set through recursive elimination, prioritizing genes that best distinguish diseased from healthy states. These algorithms are applied to primary datasets (GSE130073 for PsA, GSE163211 for Long Covid) and validated on independent datasets (GSE95065, GSE171110) to ensure generalizability. The use of **ROC curves** quantifies diagnostic accuracy, while **nomographs** provide a clinical tool for predicting disease risk based on gene expression profiles. This approach not only identifies shared molecular signatures between PsA and Long Covid but also facilitates the development of precise diagnostic models and targeted therapies, leveraging the power of data-driven insights to address complex immune-mediated diseases.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
