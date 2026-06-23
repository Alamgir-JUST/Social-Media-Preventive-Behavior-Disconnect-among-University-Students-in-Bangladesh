# The Social Media–Preventive Behavior Disconnect among University Students in Bangladesh

**A Cross-Sectional Mediation Study (Health Belief Model + Theory of Planned Behavior)**

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Made with Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange.svg)](https://jupyter.org/)
[![Code License: MIT](https://img.shields.io/badge/Code%20License-MIT-green.svg)](LICENSE)
[![Data License: CC BY 4.0](https://img.shields.io/badge/Data%20License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://img.shields.io/badge/DOI-pending-inactive.svg)](#citation)

This repository contains the data, analysis code, and supporting materials for the study examining whether social media exerts a **direct** effect on the preventive health behavior of Bangladeshi university students, or whether its influence is **fully transmitted** through health beliefs and peer norms. The manuscript has been submitted to *Heliyon* (Elsevier).

---

## Table of contents

- [Overview](#overview)
- [Key findings](#key-findings)
- [Repository structure](#repository-structure)
- [Data](#data)
- [Analysis pipeline](#analysis-pipeline)
- [Requirements](#requirements)
- [How to reproduce](#how-to-reproduce)
- [Outputs](#outputs)
- [Ethics](#ethics)
- [Citation](#citation)
- [License](#license)
- [Authors and contact](#authors-and-contact)
- [Acknowledgments](#acknowledgments)

---

## Overview

Social media is now a dominant channel through which young adults encounter health information, yet exposure does not reliably translate into preventive action — an "engagement–behavior gap" that is especially pronounced among university students. Drawing on the **Health Belief Model (HBM)** and the **Theory of Planned Behavior (TPB)**, this study tests whether social media acts on preventive behavior directly or indirectly through the cognitions and norms it cultivates.

A cross-sectional survey of **410 students** from public and private universities in Bangladesh was analyzed using reliability testing, Pearson correlation, hierarchical regression, and **bootstrapped parallel mediation**. The headline result: although social media engagement correlates with preventive behavior at the zero-order level, that association **collapses to non-significance** once health beliefs and peer norms are controlled — a pattern of **full mediation**. The practical implication is that belief- and peer-targeted digital campaigns are more promising than exposure-centric strategies.

## Key findings

| Result | Value |
|---|---|
| Sample size | N = 410 |
| Social media ↔ preventive behavior (zero-order) | r = 0.228, p < .001 |
| Social media effect after adjustment | β = −0.045, p = .39 (non-significant) |
| Health beliefs (adjusted) | β = 0.261, p < .001 |
| Peer influence (adjusted) | β = 0.280, p < .001 |
| Indirect effect via health beliefs | 0.135, 95% CI [0.077, 0.198] |
| Indirect effect via peer influence | 0.115, 95% CI [0.067, 0.168] |
| Total indirect effect | 0.250, 95% CI [0.183, 0.321] |
| Direct effect (c′) | −0.024 (non-significant) |
| Mediation conclusion | **Full mediation** |

Subgroup analyses identified on-campus and public-university students as comparatively vulnerable to low preventive engagement.

## Repository structure

```
.
├── README.md
├── LICENSE                         # MIT (code)
├── requirements.txt                # Python dependencies
├── notebooks/
│   └── Preventive_Health_Heliyon.ipynb   # Full, documented analysis pipeline
├── data/
│   ├── Preventive_Health_Behavior_Dataset.csv   # De-identified survey responses (N = 410)
│   └── data_dictionary.md          # Variable/codebook reference
├── results/
│   ├── Results_Tables.xlsx         # Tables 1–9 (auto-exported by the notebook)
│   └── Figure_SocialMedia_Disconnect.png   # Figure 2 (300 dpi)
└── docs/
    └── questionnaire.pdf           # Survey instrument (optional)
```

> Folders marked above are the recommended layout. If you keep the notebook's original Google Drive paths, update them to the relative paths shown here when running locally (see [How to reproduce](#how-to-reproduce)).

## Data

The dataset contains **410 anonymous responses** to a self-administered online questionnaire distributed to students at public and private universities in Bangladesh, collected via convenience sampling. No personally identifying information was collected; the data are suitable for public release.

The instrument comprises a demographic block and five multi-item construct blocks, plus multiple-response items on past behaviors, barriers, and endorsed strategies:

| Construct | Items | Cronbach's α | Mean | SD |
|---|---|---|---|---|
| Preventive behavior | 6 | 0.735 | 2.53 | 0.84 |
| Peer influence (TPB subjective norms) | 4 | 0.767 | 2.90 | 0.85 |
| Institutional support | 5 | 0.851 | 2.87 | 0.92 |
| Social media influence | 5 | 0.813 | 3.15 | 0.85 |
| Health beliefs (HBM) | 4 | 0.797 | 3.38 | 0.88 |

**Important preprocessing notes (reproduced faithfully in the notebook):**

- **Coding-error correction.** A form inconsistency affected 70 cells in the social-media block, where the displayed numeral contradicted the textual anchor. These were resolved in favor of the **text label** respondents actually selected.
- **Reverse-coded items.** Two negatively worded items (one peer item, one health-belief item) were reverse-coded, then **excluded** from scale construction after diagnostics showed negative corrected item–total correlations (−0.42 and −0.39). Removing them raised α for peer influence from 0.44 → 0.77 and for health beliefs from 0.52 → 0.80. Both items are retained in the dataset for transparency.
- Construct scores are the mean of their constituent items. The final dataset contains no missing values.

See [`data/data_dictionary.md`](data/data_dictionary.md) for the full variable codebook.

## Analysis pipeline

The notebook ([`notebooks/Preventive_Health_Heliyon.ipynb`](notebooks/Preventive_Health_Heliyon.ipynb)) is fully annotated and runs top to bottom. Its sections map directly to the manuscript:

1. **Environment setup & data loading** — plotting configuration, load the survey CSV.
2. **Data preprocessing (§3.4)** — column renaming, Likert encoding with the coding-error correction, reverse-coding, item–total reliability diagnostics, and final scale construction.
3. **Results (§4)**
   - Sample demographics (Table 1)
   - Construct correlations (Table 3)
   - Hierarchical OLS regression — Model 1 vs. Model 2 (Table 4)
   - Bootstrapped parallel mediation, 5,000 resamples (Table 5)
   - Regression diagnostics — VIF, Shapiro–Wilk, Breusch–Pagan
   - Subgroup comparisons — t-tests, one-way ANOVA, Cohen's d (Table 6)
   - Tukey HSD post-hoc for living arrangement
   - Multi-select behaviors, barriers, and strategies (Table 7)
4. **Figures & export** — Figure 2 (two-panel) and a multi-sheet Excel workbook of all results tables.

Statistical significance was set at α = .05 throughout.

## Requirements

The analysis was conducted in **Google Colab using Python 3** (CPU runtime). To run locally, Python 3.9+ is recommended.

`requirements.txt`:

```
pandas
numpy
scipy
statsmodels
matplotlib
openpyxl
jupyter
```

Install with:

```bash
pip install -r requirements.txt
```

## How to reproduce

### Option A — Google Colab (closest to the original environment)

1. Open the notebook in Colab.
2. Upload `Preventive_Health_Behavior_Dataset.csv`, or mount Google Drive and adjust the file path in the data-loading cell.
3. Run all cells (`Runtime → Run all`). The notebook regenerates every table and figure and exports `Results_Tables.xlsx`.

### Option B — Local Jupyter

1. Clone the repository:
   ```bash
   git clone https://github.com/Alamgir-JUST/Social-Media-Preventive-Behavior-Disconnect-among-University-Students-in-Bangladesh.git
   cd Social-Media-Preventive-Behavior-Disconnect-among-University-Students-in-Bangladesh
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. In the data-loading cell, replace the Google Drive path with the relative path:
   ```python
   df = pd.read_csv("data/Preventive_Health_Behavior_Dataset.csv")
   ```
   and point the figure/Excel export paths to `results/`.
4. Launch Jupyter and run all cells:
   ```bash
   jupyter notebook notebooks/Preventive_Health_Heliyon.ipynb
   ```

Bootstrapping uses a fixed seed (`np.random.default_rng(42)`), so the mediation confidence intervals are reproducible.

## Outputs

Running the notebook produces:

- **`Figure_SocialMedia_Disconnect.png`** — Figure 2. Panel A contrasts zero-order correlations with adjusted regression coefficients (the social-media association collapses while beliefs and peers persist); Panel B decomposes the total effect into a non-significant direct effect and significant indirect effects.
- **`Results_Tables.xlsx`** — a single workbook with nine sheets: demographics, reliability/descriptives, correlations, hierarchical regression, mediation, group comparisons, and the three multi-select tables (past behaviors, barriers, strategies).

## Ethics

Participation was voluntary and anonymous, and responses were used solely for academic purposes. No personally identifying information was collected. The study was conducted in accordance with the Declaration of Helsinki.
<!-- TODO: Add ethics approval / IRB reference number and approving body, e.g.
Ethical approval was granted by <Skill Morph Research Lab., Skill Morph, Dhaka, Bangladesh>, approval no. <SkillMorph/ES/2025/02(01)>. -->

## Citation

If you use this code or data, please cite the article (details to be finalized upon publication):

> <Author(s)>. (2026). *The Social Media–Preventive Behavior Disconnect among University Students in Bangladesh: A Cross-Sectional Mediation Study.* Heliyon. DOI: \<to be added on acceptance\>

BibTeX:

```bibtex
@article{<key>2026socialmedia,
  title   = {The Social Media--Preventive Behavior Disconnect among University Students in Bangladesh: A Cross-Sectional Mediation Study},
  author  = {<Farhana Yasmin, Md. Waresul Zannat Razu, Md. Alamgir Hossain>},
  journal = {Heliyon},
  year    = {2026},
  doi     = {<to be added on acceptance>}
}
```

## License

- **Code** (notebook and scripts): released under the [MIT License](LICENSE).
- **Data and documentation**: released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/), consistent with *Heliyon*'s open-access model.

You are free to share and adapt this material with appropriate attribution.

## Authors and contact

- **Repository maintainer:** [@Alamgir-JUST](https://github.com/Alamgir-JUST)
- **Corresponding author:** \<Md. Alamgir Hossain\>, \<SKill Morph Research Lab., Skill Morph, Dhaka, Bangladesh\> — \<alamgir.cse14.just@gmail.com\>
<!-- TODO: Add the full author list, affiliations, and ORCID iDs. -->

For questions, please open an [issue](https://github.com/Alamgir-JUST/Social-Media-Preventive-Behavior-Disconnect-among-University-Students-in-Bangladesh/issues).

## Acknowledgments

We thank the university students who participated in the survey. Analyses were performed in Python using pandas, NumPy, SciPy, statsmodels, and matplotlib.
