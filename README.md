================================================================================
SIMPLE BASELINES FOR CO₂ UPTAKE PREDICTION IN MOFs
================================================================================

Author: Vahid Safarifard
Date: May 2026
GitHub: https://github.com/vahidsafarifard/MOF-CO2-baseline

================================================================================
GRAPHICAL ABSTRACT
================================================================================

[Image: figures/graphical_abstract.png]
Simple Random Forest with 7 textural features outperforms complex GNN

================================================================================
OVERVIEW
================================================================================

Using only 7 textural properties and a Random Forest:

  Pressure    Model              PCC      MAE (g/kg)    R²
  ----------  -----------------  -------- ------------  ------
  50 bar      Linear Regression  0.9801   18.0          0.96
  50 bar      Random Forest      0.9987   17.4          0.997
  1 bar       Random Forest      0.8926   15.3          0.79

================================================================================
KEY FINDING
================================================================================

> At high pressure (1-50 bar), CO₂ uptake is almost entirely determined by 
> pore geometry. Complex graph neural networks may be unnecessary.

================================================================================
WHY THIS MATTERS
================================================================================

  Simplicity      : Only 7 features, no atomic coordinates
  Speed           : Training takes ~2 seconds on a laptop
  Interpretability: Feature importance reveals what matters
  Performance     : Beats published GNN results at high pressure

================================================================================
REPOSITORY CONTENTS
================================================================================

  MOF-CO2-baseline/
  ├── README.txt                       # This file
  ├── IsothermNet_Reproduction.ipynb   # Jupyter notebook
  ├── results_summary.csv              # Summary of results
  ├── requirements.txt                 # Python dependencies
  └── figures/
      ├── graphical_abstract.png       # Graphical abstract
      ├── parity_plots_50bar.png       # Predictions at 50 bar
      ├── parity_plot_1bar.png         # Predictions at 1 bar
      ├── feature_importance.png       # Feature importance
      └── error_analysis.png           # Error distribution

================================================================================
FIGURES
================================================================================

Figure 1: Parity Plot at 50 Bar
[Image: figures/parity_plots_50bar.png]

Figure 2: Parity Plot at 1 Bar
[Image: figures/parity_plot_1bar.png]

Figure 3: Feature Importance
[Image: figures/feature_importance.png]

Figure 4: Error Distribution
[Image: figures/error_analysis.png]

================================================================================
FEATURE IMPORTANCE RANKING
================================================================================

  Rank  Feature                Importance
  ----  --------------------   ----------
  1     Density                0.8671
  2     Void Fraction          0.1164
  3     Surface Area           0.0102
  4     Channel Volume         0.0049
  5     PLD                    0.0008
  6     LCD                    0.0005
  7     No. Channels           0.0000

================================================================================
ERROR DISTRIBUTION
================================================================================

  Mean error         : 18.03 g/kg
  Median error       : 12.07 g/kg
  90th percentile    : 39.10 g/kg
  Max error          : 424.84 g/kg

================================================================================
LEAKAGE CHECKS (ALL PASSED)
================================================================================

  [✓] Train/test feature distributions are similar
  [✓] Pore volume proxy matches between train and test
  [✓] No duplicate MOFs between train and test
  [✓] Best single feature PCC = 0.9064

================================================================================
PHYSICAL INTERPRETATION
================================================================================

At high pressure (50 bar), CO₂ uptake is dominated by pore filling:

  Uptake ≈ k × (Void Fraction / Density)

This explains why:

  - Density is the most important feature (correlation: -0.81)
  - Surface area and pore volume are also highly predictive
  - Atomic details matter less at high pressure

================================================================================
REQUIREMENTS
================================================================================

  pip install torch pandas numpy matplotlib seaborn scikit-learn scipy

================================================================================
HOW TO RUN
================================================================================

  1. Clone the repository
  2. Download data files to the same directory
  3. Open IsothermNet_Reproduction.ipynb in Jupyter
  4. Run all cells

================================================================================
DATA FILES
================================================================================

  File                           Shape        Description
  -----------------------------  -----------  ---------------------------------
  texturalProperties_vol.xlsx    (5394, 8)    MOF IDs + 7 textural features
  y_dataset19.pth                (5394, 19)   CO₂ uptake at 19 pressures
  H_dataset.pth                  (5394, 19)   Heat of adsorption (not used)

Pressure points (19 columns):

  Col 0  = 0.01 bar    Col 5  = 2.0 bar     Col 10 = 10 bar     Col 15 = 35 bar
  Col 1  = 0.05 bar    Col 6  = 3.0 bar     Col 11 = 15 bar     Col 16 = 40 bar
  Col 2  = 0.1 bar     Col 7  = 4.0 bar     Col 12 = 20 bar     Col 17 = 45 bar
  Col 3  = 0.5 bar     Col 8  = 5.0 bar     Col 13 = 25 bar     Col 18 = 50 bar
  Col 4  = 1.0 bar     Col 9  = 7.0 bar     Col 14 = 30 bar

================================================================================
LIMITATIONS
================================================================================

  [ ] Low pressure (<1 bar): Not tested; surface chemistry may dominate
  [ ] Heat of adsorption: Not tested (data units unclear)
  [ ] Generalization: Results on QMOF database only

================================================================================
CITATION
================================================================================

  @misc{MOFCO2Baseline2026,
    author = {Vahid Safarifard},
    title = {Simple Baselines for CO₂ Uptake Prediction in MOFs},
    year = {2026},
    publisher = {GitHub},
    url = {https://github.com/vahidsafarifard/MOF-CO2-baseline}
  }

================================================================================
LICENSE
================================================================================

MIT License

================================================================================
CONTACT
================================================================================

https://www.linkedin.com/in/vahid-safarifard-018206153/

================================================================================
ACKNOWLEDGMENTS
================================================================================

  - QMOF database for MOF structures
  - IsothermNet authors for public data

================================================================================
