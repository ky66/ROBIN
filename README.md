
# Machine Learning Informs RNA-Binding Chemical Space

**<ins>R</ins>epository <ins>O</ins>f <ins>BI</ins>nders to <ins>N</ins>ucleic acids (ROBIN)** is a new experimentally-derived nucleic acid binding small molecule library. This chemical library was curated by small molecule microarray (SMM) screening of 36 nucleic acid targets against a library of 24,572 small molecules. Here, we have included the code used for generation of machine learning models and figures published in the following paper:  <br>
(https://www.biorxiv.org/content/10.1101/2022.08.01.502065v1.full.pdf)


# Directories

## notebooks
This directory contains the following jupyter notebooks:
1. <ins>ML_Models_ROBIN_RNA_vs_FDA.ipynb</ins>: 
This notebook contains the code used for comparison of the ROBIN RNA binders with a set of FDA-approved drugs. 
2. <ins>ML_Models_ROBIN_RNA_vs_BindingDB.ipynb</ins>: 
This notebook contains the approach used for classification of the ROBIN RNA binders and BindingDB protein binders. 
3. <ins>MLP_Model_Run.ipynb</ins>: 
This notebook contains the code required to run new compounds using the MLP model to predict the chance of RNA over protein binding. 

## figures

This is the directory used for depositing figures produced by the python code in the notebooks directory. 


## data

Since the starting datasets used for machine learning are large, they are deposited in Figshare at the following URL
(https://doi.org/10.6084/m9.figshare.20401974). After cloning this repository, the folders from Figshare should be copied to the data directory of this github respository to be used in the jupyter notebooks. The mentioned Figshare URL includes the following folders:
1. <ins>SDF_files</ins>: 
This folder contains the SDF files of the compounds used in machine learning models. The SDF_files folder contains the following files:

    a) BindingDB_3D.sdf: This file contains protein binders from BindingDB used for classification of RNA- and protein-binding compounds. 
    
    b) FDA_Approved_3D.sdf: This file contains a set of FDA-approved drugs extracted from Selleck Chemicals used for classification of RNA binding compounds and FDA-approved drugs. 

    c) ROBIN_DNA_and_RNA_Binders_3D.sdf: This file contains the entire collection of compounds in the ROBIN library which bound to at least one DNA or RNA target on SMM. 

    d) ROBIN_Plus_3D.sdf: This file contains the compounds extracted from the ZINC database used to augment RNA binders in classification of RNA and protein binders. 

    e) ROBIN_RNA_Binders_3D.sdf: This file contains the compounds from ROBIN that bound to at least one RNA target. 

    f) SMM_All_Compounds_3D.sdf: This file contains the entire composition of the SMM  library used to screen nucleic acid targets. 

    g) SMM_RNA_Non_Binder_3D.sdf: This file contains the collection of compounds screened via SMM that did not bind to any RNA target. 

    h) Test_Compounds_3D.sdf: The file contains 8 compounds from the literature with well-characterized RNA- or protein-binding activity used to validate the performance of the RNA/protein binding classifier described in the paper. 

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


## MLP_saved_model
This directory contains the architecture and weights of the final MLP model to be run on new compounds to predict the chance of RNA over protein binding. 


## Substructure_searching
This directory contains the substructures used for substructure enrichment analysis of ROBIN RNA binders performed in the paper. More details can be found in the methods and results section of the paper. 

## TMAP
This directory contains the interactive HTML file of the TMAP shown in the paper. Included are two versions of the heatmaps. 



# Generation of Mordred chemical descriptors from SDF files

The command-line version of [Mordred](https://github.com/mordred-descriptor/mordred) package (version 1.2.0) was used as following on each 3D SDF file:

<pre>
python -m mordred -3 [SDF file] -o [output CSV file]
</pre>

--Please note that the Mordred package uses an RDKit backend. The RDkit version used for generation of Mordred descriptors was 2018.09.1. First, make a new conda environment and install RDKit on there using the command (conda install -c rdkit rdkit=2018.09.1). 

--Also, based on testing on multiple computers, the prediction of models might not be exactly the same with the same packages installed. We observed about 1% variability in predictions run by different lab members with the same packages installed. 

# How to use the MLP model on new compounds
First, prepare an SDF file of your compounds and generate a single 3D conformer for each compound using DataWarrior’s “Generate Conformers” functionality. Use DataWarrior’s “Systematic, low energy bias” algorithm to minimize energy using the MMFF94s+ forcefield with initial torsions adjusted to “From crystallographic database”. After the generation of 3D conformers, use ICM-Pro (version 3.9) modeling software (MolSoft LLC) to remove salts and explicit hydrogens (Chemistry/Standardize/Remove Salts, Remove Explicit Hydrogens) from each compound. In addition, standardize groups and tautomers to ensure consistency of the chemical structures (Chemistry/Standardize/Standardize Groups, Standardize Tautomers). Next, set formal charges for ionizable groups at pH 7.4 consistent with the pH used in our SMM screening buffers (Set Formal Charges/Auto Using pKa Model/pH Value:7.40).

After generation of the cleaned SDF file, generate the Mordred features CSV file from the SDF file as described above. Then, read in the resulting CSV file into the MLP_Model_Run.ipynb notebook in the notebooks folder and follow the instructions in this notebook to predict the chance of RNA over protein binding of your desired compounds. 

