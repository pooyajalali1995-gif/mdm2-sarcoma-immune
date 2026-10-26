# MDM2 amplification and the immune microenvironment in sarcoma

Code for an ongoing project on how MDM2 amplification (together with the rarer MDM4 amplification) relates to tumor mutational burden, the immune microenvironment and survival in sarcoma, using public genomic, transcriptomic and single-cell data.

## Contents

`MDM2_sarcoma_immune.ipynb` is a single Google Colab notebook, saved with its outputs, that runs the full analysis:

1. **Download** TCGA-SARC (clinical, GISTIC copy number, RNA-seq) and MSK-IMPACT 50K sarcoma samples (TMB, MDM2/MDM4/CDK4 copy number) from the cBioPortal REST API.
2. **TCGA-SARC:** Treg, cytotoxic, macrophage and T-cell scores by amplification status with histology-adjusted regression; Cox models (implemented with numpy/scipy) for amplification and for immune balance, adjusted for histology, age and amplification; CDK4 co-amplification.
3. **MSK-IMPACT 50K:** TMB in amplified vs non-amplified sarcomas, MDM2-only sensitivity analysis, non-liposarcoma subset and histology-adjusted rank regression.
4. **GSE221493 (liposarcoma scRNA-seq atlas):** per-sample MDM2 expression in tumor cells vs Treg abundance, in all samples, tumor-only, per patient, and paired dedifferentiated vs well-differentiated components.

## Running

Open the notebook in [Google Colab](https://colab.research.google.com) and choose Runtime > Run all. No installation is needed. The single-cell step downloads about 650 MB from GEO and needs about 6 GB RAM.

## Main results so far

- **MSK-IMPACT (n=2,897 soft tissue and bone sarcomas):** amplified tumors have lower TMB (median 0.88 vs 1.12, p<1e-15); the difference persists after adjustment for detailed histology. CDK4 is co-amplified in 86% of amplified tumors.
- **TCGA-SARC:** amplified tumors have higher Treg infiltration after histology adjustment (p=0.002), together with more T cells overall. A higher cytotoxic-to-Treg balance predicts better overall survival independently of histology, age and amplification (HR 0.69 per SD, p=0.002).
- **GSE221493:** in tumor samples, MDM2 expression in tumor cells correlates with the Treg fraction of T cells (rho=0.42, p=0.04); within patients, dedifferentiated components express more MDM2 and contain more Tregs than paired well-differentiated components (6 of 7 patients).

## Notes and limitations

- MDM2 amplification is concentrated in liposarcoma, so histology is a strong confounder; all key comparisons are reported with and without histology adjustment.
- TCGA patients were not treated with immune checkpoint inhibitors, so TCGA survival results are prognostic, not predictive.
- In the single-cell data, the patient-level correlation (one value per patient) is not significant; the dataset is small.

## Data sources

- TCGA-SARC PanCancer Atlas and MSK-IMPACT 50K via [cBioPortal](https://www.cbioportal.org)
- [GSE221493](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE221493): single-cell atlas of dedifferentiated and well-differentiated liposarcoma

No patient-level data are stored in this repository.
