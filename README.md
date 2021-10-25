# ecg_diagnosis

## Data

The data is obtained from https://physionetchallenges.org/2021/

To run the jupyter notebooks, save the databases in the following folder names:
1. CPSC Database: data/cpsc
2. CPSC-Extra Database: data/cpsc2
3. PTB-XL Database: data/ptbxl
4. The Georgia 12-lead ECG Challenge (G12EC) Database: data/georgia
5. Chapman-Shaoxing Database: data/chapman
6. Ningbo Database: data/ningbo

## Data Processing

The jupyter notebook data_exploration.ipynb cosnsists of the steps to generate a dataframe that consists of the filenames of each ECG recording and the relevant labels attached to it. It produces the csv "full_dataset.csv".

## Model Training and Prediction

3 models were trained to predict Atrial Fibrillation (afib_model.ipynb), Atrial Flutter (afl_model.ipynb), and Myocardial Infarction (mi_model.ipynb).

Running their respective jupyter notebooks after generating the "full_dataset.csv" file will execute the steps required to train the model.

After training, an out-of-sample test set partitioned out before the training steps were executed was used to evaulate the performance of the model. The results are as follows:
1.  Atrial Fibrillation: Sensitivity = 95%, Specificity = 85%
2.	Atrial Flutter: Sensitivity = 91%, Specificity = 98%
3.	Myocardial Infarction: Sensitivity = 99%, Specificity = 72%
