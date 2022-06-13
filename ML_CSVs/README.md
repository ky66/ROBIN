This folder will be filled with CSVs generated from jupyter notebooks as machine learning models are run. This directory ensures rerunning
machine learning models does not require rerunning the data preparation steps. 

*The scaler.pkl file includes the parameters of the standardscalar() that will be used to standardize new compound features for running the MLP model on new compounds. This picke is used in the MLP_Model_Run.ipynb notebook in the notebooks folder. 