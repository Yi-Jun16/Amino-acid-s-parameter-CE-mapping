Code and data for amino acid contact-electrification analysis

Overview: This repository provides selected Python code and data for analysing the contact-electrification response of twenty canonical amino acids. The workflow includes descriptor comparison, regression analysis, non-nested and nested leave-one-out cross-validation (LOOCV), bootstrap analysis and Prediction Priority Score (PPS) calculation.

Files: amino_acid_ce.py contains the analysis code, training data and model settings. README.md provides installation and usage instructions. No separate data file is required. Derivative-specific datasets are not included.

Data: The molecular descriptors comprise LUMO, HOMO, their energy gap and six group-resolved condensed Fukui indices. Orbital energies are reported in eV, whereas Fukui indices are dimensionless. The response variable is measured open-circuit voltage in V, without target normalization. Predictions, bootstrap standard deviations, MAE and RMSE are in V; R² and standardized descriptor distances are dimensionless.

The script reports descriptor-set comparisons, selected parameters, regression performance and permutation importance. Model comparisons are conditional on the implemented configurations.

Validation includes the complete twenty-molecule dataset and the post hoc seventeen-molecule subset omitting CYS, MET and TYR. Descriptor selection and hyperparameter optimization use only outer-training data in the nested reselection analysis. Standardization is fitted within training folds.

PPS combines predicted voltage, bootstrap uncertainty and the nearest-training Euclidean distance in standardized selected-descriptor space:
PPS = 100 × clip(V_pred / V_ref, 0, 1) / [(1 + α × SD)(1 + 0.8 × distance)]
V_ref = 1 V; α = 5 V⁻¹.

Clipping applies only to the scoring factor. pps_ranking.csv ranks candidates by PPS. screened_prediction_ranking.csv applies SD < 0.15 V and distance < 0.8, then ranks candidates by predicted voltage.
Reproducibility: Bootstrap analysis uses 500 resamples and seed 42, with descriptors and hyperparameters fixed while the scaler and SVR are refitted in each resample. Bootstrap quantiles describe conditional model variability rather than guaranteed coverage of new measurements. Permutation importance uses 100 repeats and seed 42 on the fitted training model. 

Citation and contact: Please cite the associated article when using this code or dataset. For questions, contact the 'haoyijun@u.nus.edu'.
