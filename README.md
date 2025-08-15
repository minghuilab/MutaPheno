# MutaPheno
An Interpretable Molecular Phenotype-Based Classifier for Predicting Pathogenic and Cancer Driver Missense Mutations

## About
MutaPheno is an interpretable machine learning tool designed to predict both pathogenic and cancer driver missense mutations. It integrates 34 molecular phenotype-based features across three biological levels: residue, mutation, and protein, spanning structural, functional, physicochemical, and contextual dimensions. 
Using an optimized random forest classifier trained through extensive grid search and cross-validation, MutaPheno delivers robust and generalizable performance. By quantifying feature pattern enrichment between pathogenic and benign mutations via log₁₀ odds ratios, the tool achieves both high interpretability and strong predictive power.
The tool accepts a list of missense mutations with corresponding protein identifiers and outputs:
•	Pathogenicity predictions (probabilities and binary labels)
•	Detailed feature annotations
Benchmarking demonstrates MutaPheno's superior accuracy and interpretability compared to existing methods, establishing it as a general-purpose predictor for both inherited disease and cancer mutations.

## MutaPheno Installation and Usage Instructions
