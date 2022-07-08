Aug 2021 - June 2022
# Automated ECG Diagnosis with ResNet

Heart conditions affect 500 million people yearly, and a 12-Lead Electrocardiogram (ECG) is one of the best ways to diagnose them effectively. However, interpreting an ECG usually requires a specialist, who are too busy to monitor patients constantly. This ResNet Model can automatically diagnose conditions from ECGs with human-level accuracy, so that busy doctors can be alerted when patients require attention.

This model has been trained on 4 important conditions: Atrial Fibrillation (AFib), Atrial Flutter (AFl), Supraventricular Tachycardia (SVT), and Myocardial Infarction (MI). Their Sensitivity (Sn), or true-positive, and Specificity (Sp), or true-negative, rates on out-of-sample test sets are below:
```
AFib -  Sn: XX%, Sp: XX%
AFl  -  Sn: XX%, Sp: XX%
SVT  -  Sn: XX%, Sp: XX%
MI:  -  Sn: XX%, Sp: XX%
```
Refer to this README for a quick summary of the implementation, or view the notebooks for an in-depth description.

## Data & Preprocessing

A total of 121,149 12-Lead ECG tracings from different patients were obtained from the following open-source databases:
```
1. CPSC Database: 13,256
2. INCART Database: 74
3. PTB and PTB-XL Database: 22,353
4. Georgia ECG Database: 20,672
5. Chapman-Shaoxing and Ningbo Database: 45,152
6. UMich Database: 19,642
```
The data can be downloaded from https://physionetchallenges.org/2021/. A sample of a 12-Lead ECG as displayed on a conventional hospital ECG paper would look something like this:

![ECG_Sample](images/ecg_sample.png)

The preprocessing included reading the ECG metadata from the associated .mat files, before filtering out tracings which had unsuitable lenghts or data formats. As the actual ECG data files were large, only the filepaths and metadata was used to preprocess the data. A DataFrame of the final dataset was constructed that included the filepath and the labels for the 4 conditions mentioned, and then saved into the CSV file "full_dataset.csv".

## ResNet Model Overview

A ResNet employs skip-connections to mitigate the problem of vanishing gradients and allow for larger and larger models to train well. A simple illustration of a skip-connection is shown below:

![resnet](images/resnet.png)

A 1D CNN ResNet was used, with 3 Residual blocks used for a relatively small model of less than 500,000 weights. It was trained from scratch on the ECG data, as there are no suitable transfer learning models available.

## Model Training and Prediction

3 models were trained to predict Atrial Fibrillation (afib_model.ipynb), Atrial Flutter (afl_model.ipynb), and Myocardial Infarction (mi_model.ipynb).

Running their respective jupyter notebooks after generating the "full_dataset.csv" file will execute the steps required to train the model.

After training, an out-of-sample test set partitioned out before the training steps were executed was used to evaulate the performance of the model. The results are as follows:
1.  Atrial Fibrillation: Sensitivity = 95%, Specificity = 85%
2.	Atrial Flutter: Sensitivity = 91%, Specificity = 98%
3.	Myocardial Infarction: Sensitivity = 99%, Specificity = 72%

## Model Usage

The trained models are stored in the folder "models" and can be executed by running the commands in the last section of the respective jupyter notebook files for each model.
