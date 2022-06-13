
# ROBIN: An Experimentally-derived Nucleic Acid Binding Library Informs RNA-binding Chemical Space

**<ins>R</ins>epository <ins>O</ins>f <ins>BI</ins>nders to <ins>N</ins>ucleic acids (ROBIN)** is a new experimentally-derived nucleic acid binding small molecule library. This chemical library was curated by small molecule microarray (SMM) screening of 36 nucleic acid targets against a library of 24,579 small molecules. Here, we have included the code used for generation of machine learning models and figures published in the following paper:  <br>
[put the DOI of the paper]


# Directories

## notebooks
This directory contains the following jupyter notebooks:
1. <ins>ML_Models_ROBIN_RNA_vs_FDA.ipynb</ins>: 
This notebook contains the code used for comparison of the ROBIN RNA binders with a set of FDA-approved drugs. 
2. <ins>ML_Models_ROBIN_RNA_vs_BindingDB.ipynb</ins>: 
This notebook contains the approach used for classification of the ROBIN RNA binders and BindingDB protein binders. 

## figures

This is the directory used for depositing figures produced by the python code in the notebooks directory. 


## data

Since the starting datasets used for machine learning are large, they are deposited in figshare at the following URL
([put figshare url]). After cloning this repository, the folders from figshare should be copied to the data directory of this github respository to be used in the jupyter notebooks. The mentioned fishare URL includes the following folders:
1. <ins>SDF_files</ins>: 
This folder contains the SDF files of compounds used in machine learning models. 
2. <ins>Mordred_files</ins>: 
This folder contains CSV files of Mordred chemical descriptors derived from SDF files mentioned above. 

## ML_CSVs
This directory contains several folders and files used in different stages of machine learning models used in the jupyter notebooks. 

## LASSO_coefficients
This directory contains the coefficients of logistic regression models used throughout the machine learning analysis. 

## SMM_full_results
This directory contains full results of small molecule microarray (SMM) screening against 36 nucleic acid targets. Four files are included in this directory as following:
1. SMM_Biomolecule_Hits.csv: This CSV file contains information about whether each SMM molecule was a hit for any nucleic acid, RNA, DNA, or G-quadruplex. 
2. SMM_Sequence_Table_hit_rates.csv: This CSV file contains information about each nucleic acid target screened via SMM. Included are sequence, structure type, and hit rates for each nucleic acid target. 
3. SMM_Target_Hits.csv: This file contains information about whether each SMM compound was a hit for each nucleic acid target. 
4. SMM_Zscore_CV.csv: This file contains the raw results of SMM screening against each nucleic acid target. For each compound, two replicate spots were printed on the slide. The results of each SMM screen is reported as following:
a) Z_score_treated: Initial average Z-score of replicate compound spots on the slide b) Z-final: Initial Z-score of each compound subtracted from the Z-score of the compound on the buffer slide to remove the effect of autofluorescent compounds. c) CV: Coefficient of variation of two replicate compound spots on the slide. 


# Generation of Mordred chemical descriptors from SDF files

The command-line version of [Mordred](https://github.com/mordred-descriptor/mordred) package (version 1.2.0) was used as following on each 3D SDF file:


<pre>
python -m mordred -3 [SDF file] -o [output CSV file]
</pre>
