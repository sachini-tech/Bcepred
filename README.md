# BcePred: Prediction of Continuous B-Cell Epitopes in Antigenic Sequences Using Physico-chemical Properties

Welcome to the official repository for BcePred, a web server for predicting continuous B-cell epitopes in antigenic protein sequences. This resource is designed to support researchers in vaccine design, immunoinformatics, and computational immunology.

Web Server:  https://webs.iiitd.edu.in/raghava/bcepred/

ZENODO : https://doi.org/10.5281/zenodo.20112047

## Citation

Saha, S., & Raghava, G. P. S. (2004).
BcePred: Prediction of continuous B-cell epitopes in antigenic sequences using physico-chemical properties.
In G. Nicosia, V. Cutello, P. J. Bentley, & J. Timmis (Eds.),
*Artificial Immune Systems, Third International Conference (ICARIS 2004)*,
Lecture Notes in Computer Science, Vol. 3239, pp. 197–204.
Springer-Verlag Berlin Heidelberg.

https://link.springer.com/chapter/10.1007/978-3-540-30220-9_16

## About the Tool

BcePred is a web-based server for predicting continuous (linear) B-cell epitopes in antigenic protein sequences using physico-chemical properties of amino acids. It provides a systematic, benchmarked evaluation of seven residue property scales commonly used in existing epitope prediction methods — and introduces a combined multi-property approach that outperforms any single property.

The tool integrates data from:

* Bcipep database (experimentally validated B-cell epitopes)
* SWISS-PROT database (non-epitope random peptide sequences)


## Key Features

### Dataset

* 1,029 non-redundant continuous B-cell epitopes from the Bcipep database
* 1,029 non-epitopes (random peptides of equal length, derived from SWISS-PROT)
* Coverage across diverse pathogenic groups: viruses, bacteria, protozoa, and fungi

### Physico-chemical Properties Evaluated

| Property | Reference | Best Accuracy |
|---|---|---|
| Hydrophilicity | Parker et al., 1986 | 54.47% |
| Accessibility | Emini et al., 1985 | 55.49% |
| Flexibility | Karplus & Schulz, 1985 | 57.53% |
| Exposed Surface | Janin & Wodak, 1978 | 55.73% |
| Polarity | Ponnuswamy et al., 1980 | 54.08% |
| Turns | Pellequer et al., 1993 | 52.92% |
| Antigenic Scale | Kolaskar & Tongaonkar, 1990 | 55.59% |

### Combined Property Performance

| Combination | Threshold | Sensitivity | Specificity | Accuracy |
|---|---|---|---|---|
| Flexibility + Hydrophilicity | 2.00 | 53% | 64% | 58.31% |
| + Polarity | 2.30 | 50% | 68% | 58.70% |
| + Surface (best combo) | 2.38 | 56% | 61% | **58.70%** |
| + Turns | 2.38 | 59% | 58% | 58.41% |
| + Accessibility | 2.38 | 60% | 56% | 57.97% |


## Overview

BcePred provides:

* Evaluation of seven established physico-chemical property scales
* Multi-property combination for enhanced prediction accuracy
* Graphical output (residue property profile plotted along protein backbone)
* Tabular output (normalized scores, max/min/average values per residue)
* User-selectable residue property, threshold, and combination options
* Threshold-dependent (sensitivity, specificity, accuracy) and independent (ROC) performance measures


## Methods Summary

### Dataset Preparation

Continuous B-cell epitopes were obtained from the Bcipep database. All identical and non-immunogenic peptides were removed, yielding 1,029 unique experimentally validated epitopes. An equal number of non-epitopes were randomly generated from SWISS-PROT at matching lengths and amino acid frequencies.

### Normalization Procedure

All property scales were normalized to a range of +3 to –3 using the following formula:

```
Normalization Score = (AMS / DS) × 6
```

Where AMS = average of the seven maximum/minimum values from the scale, and DS = difference between the maximum and minimum scores. This allows direct comparison across different property scales.

### Individual Property Methods

Each property scale uses a sliding window approach (typically 7 residues). Key methods include:

* **Parker (Hydrophilicity):** HPLC peptide retention time-based hydrophilicity scale; window of 7 residues, value assigned to the 4th (i+3) residue.
* **Karplus (Flexibility):** Flexibility scale based on B-factors of α-carbons from 31 known protein structures; 3-scale variant (3Karplus) used; window of 6 residues.
* **Emini (Accessibility):** Surface probability calculated as a product formula over hexapeptide windows; Sn > 1.0 indicates surface-exposed region.
* **Pellequer (Turns):** β-turn incidence scale; Gaussian smoothing applied over 7-residue window with weights (0.05/0.11/0.19/0.22/0.19/0.11/0.05).
* **Kolaskar (Antigenic Propensity):** Scale derived from 156 antigenic determinants in 34 proteins; frequency-based propensity values assigned per residue.
* **Exposed Surface & Polarity:** Two newly evaluated scales using 7-residue arithmetic mean windows.

### Combined Approach (BcePred Default)

The best-performing combination — **Flexibility + Hydrophilicity + Polarity + Exposed Surface** — at a threshold of 2.38 achieves:
* Accuracy: 58.70%
* Sensitivity: 56%
* Specificity: 61%

ROC analysis confirmed flexibility as the single best-performing property, consistent across thresholds.


## Improvements Over Existing Methods

* First large-scale, uniform benchmarking of all major B-cell epitope prediction property scales on an independent, non-redundant dataset
* Introduction of non-epitopes (random SWISS-PROT peptides) as negative controls — previously absent in most evaluations
* Two new properties (polarity and exposed surface area) evaluated for the first time in this context
* Web server interface allowing flexible property selection, combination, and threshold tuning
* Graphical visualization of epitope profiles along protein sequences


## Limitations

* Overall prediction accuracy for all methods is modest (52–59%), highlighting the inherent difficulty of continuous B-cell epitope prediction
* Methods tested on small datasets in prior literature tended to overestimate performance due to lack of true negative controls
* Physico-chemical properties alone do not capture the full complexity of antibody-antigen interactions
* No existing database of experimentally confirmed B-cell non-epitopes at the time of publication


## Applications

* Peptide vaccine design and candidate epitope identification
* Disease diagnosis using predicted immunodominant regions
* Benchmarking and comparison of epitope prediction tools
* Development and training of improved machine learning-based epitope predictors
* Analysis of antigenic variation in pathogenic proteins


## Contact & Authors

Prof. G. P. S. Raghava**
Bioinformatics Centre, Institute of Microbial Technology
Sector 39A, Chandigarh, India
raghava@imtech.res.in
https://webs.iiitd.edu.in/raghava/bcepred/
 


## License

Published as part of:
*Lecture Notes in Computer Science, Vol. 3239*
© Springer-Verlag Berlin Heidelberg 2004

All rights reserved. Reproduction permitted only under Springer copyright terms.
