
# ROBIN: An Experimentally-derived Nucleic Acid Binding Library Informs RNA-binding Chemical Space

**<ins>R</ins>epository <ins>O</ins>f <ins>BI</ins>nders to <ins>N</ins>ucleic acids (ROBIN)** is a new experimentally-derived nucleic acid binding small molecule library. This chemical library was curated by small molecule microarray (SMM) screening of 36 nucleic acid targets against a library of 24,579 small molecules. Here, we have included the code used for generation of machine learning models and figures published in the following paper:  <br>
[put the DOI of the paper]


# Directories

## notebooks
This directory contains the following jupyter notebooks:
1. <ins>ML_Models_ROBIN_RNA_vs_FDA.ipynb</ins>: 
This notebook contains the code used for comparison of the ROBIN RNA-binding library with a set of FDA-approved drugs. 
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

# Generation of Mordred Chemical Descriptors from SDF files

The command-line version of [Mordred](https://github.com/mordred-descriptor/mordred) package (version 1.2.0) was used as following on each 3D SDF file:


<pre>
python -m mordred -3 [SDF file] -o [output CSV file]
</pre>
