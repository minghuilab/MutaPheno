# MutaPheno
An Interpretable Molecular Phenotype-Based Classifier for Predicting Pathogenic and Cancer Driver Missense Mutations.

## About
MutaPheno is an interpretable machine learning tool designed to predict both pathogenic and cancer driver missense mutations. It integrates 34 molecular phenotype-based features across three biological levels: residue, mutation, and protein, spanning structural, functional, physicochemical, and contextual dimensions. 
Using an optimized random forest classifier trained through extensive grid search and cross-validation, MutaPheno delivers robust and generalizable performance. By quantifying feature pattern enrichment between pathogenic and benign mutations via log₁₀ odds ratios, the tool achieves both high interpretability and strong predictive power.
The tool accepts a list of missense mutations with corresponding protein identifiers and outputs:

•	Pathogenicity predictions (probabilities and binary labels)

•	Detailed feature annotations

Benchmarking demonstrates MutaPheno's superior accuracy and interpretability compared to existing methods, establishing it as a general-purpose predictor for both inherited disease and cancer mutations.

## MutaPheno Installation and Usage Instructions
### 1.	Pull Docker Image
Ensure Docker is installed: Docker Installation Guide 
(https://docs.docker.com/get-started/get-docker/)
```
docker pull minghuilab/mutapheno:v1
```

•  Image size: 68.5 GB

•  Estimated download time (approximate):
   •	100 Mbps: ~90 min
   •	1 Gbps: ~9 min
(actual time depends on your network speed)

### 2.	Run the Docker Container and Activate Environment
```
docker run -it minghuilab/mutapheno:v1 /bin/bash
conda activate py38
cd mutapheno
```

### 3.	Preparing Input Files
Inside the Docker container, create a folder to store input files:
```
mkdir -p /mutapheno/input_folder
```
Alternatively, use the predefined directory: `/mutapheno/mutapheno_input` for input file storage. 
Prepare input mutations in one of the following formats:
 (1) UniProt (default): 
Input example (example_uniprot.csv):
```
P21359-2|R1276P
P04637|H178Q
P27986|G376R
P04637|I251S
```
Command:
```
python MutaPheno.py \
  --input /mutapheno/mutapheno_input/example_uniprot.csv \
  --input_mutatype UniProt \
  --output /mutapheno/mutapheno_output
```
(2) Ensembl (Transcript/Protein): 
```
Input example (example_ensembl.csv):
ENST00000227163|P127T
ENST00000334192|A287T
ENSP00000366506|V39I
```
Command:
```
python MutaPheno.py \
  --input /mutapheno/mutapheno_input/example_ensembl.csv \
  --input_mutatype Ensembl \
  --output /mutapheno/mutapheno_output
```
 (3) RefSeq (Transcript/Protein): 
Input example (example_refseq.csv):
```
NM_000267|R1276P
NP_722540|D18T
```
Command:
```
python MutaPheno.py \
  --input /mutapheno/mutapheno_input/example_refseq.csv \
  --input_mutatype RefSeq \
  --output /mutapheno/mutapheno_output
```
**(4) Gene Name:** 

Input example (example_gene.csv):
```
BRAF|Y472C
BRCA1|C24R
EGFR|D837A
POLE|P172S
```
**Command:**
```
python MutaPheno.py \
  --input /mutapheno/mutapheno_input/example_gene.csv \
  --input_mutatype GeneName \
  --output /mutapheno/mutapheno_output
```
**Important Notes: **

Do not mix formats. Verify mutation identifiers, residue positions, and amino acid changes. Only validated missense mutations proceed to annotation and prediction. Output Files

### 4.	Understanding Output Files
After running, two main outputs will be produced in the specified output directory:

**•	Feature Annotation (`*_MutaPheno_FeatureAnnotations.csv`):**

Contains raw feature annotation data for each mutation.

**•	Prediction Results (`*_MutaPheno_Predictions.csv`):**
```
Original_Mutation	Canonical_Mutation	MutaPheno_score	MutaPheno_label
P21359-2|R1276P	P21359_R1276P	0.532308	1
P04637|H178Q	P04637_H178Q	0.563077	1
P27986|G376R	P27986_G376R	0.830769	1
P04637|I251S	P04637_I251S	0.889231	1
```
  •	**MutaPheno_score:** Probability of pathogenicity (0–1)
  
  •	**MutaPheno_label:** Binary pathogenicity classification (threshold=0.5)

**•	Feature Contribution (`*_MutaPheno_feature_SHAP.csv`):**

  •	Contains feature SHAP data for each mutation.
  
  •	SHAP (SHapley Additive exPlanations) values quantify the contribution of each feature to the model’s prediction. A positive SHAP value indicates that the feature increases the likelihood of the predicted outcome, whereas a negative SHAP value suggests it decreases the likelihood.

### 5.	Recommended System Requirements

•	RAM: ≥32 GB recommended (≥16 GB minimal requirement)

•	Disk Space: ≥100 GB (Docker image: ~68.5 GB + additional space for data and output)

