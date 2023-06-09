# cs598_dlh_patient_trajectory_prediction

## The original GitHub repository
[JamilProg/patient_trajectory_prediction](https://github.com/JamilProg/patient_trajectory_prediction/blob/master/README.md)

## Download the data from MIMIC III data

We are using the MIMIC III data. We have requested access to data by following the mandatory training. After getting the approval, we downloaded the required files. This paper only needed the below subset of files:
NOTEEVENTS.csv
ADMISSIONS.csv
DIAGNOSES_ICD.csv


## Install the required packages
```
python3 -m venv venv  
source venv/bin/activate  
pip install -r requirements.txt  

```

## Data Preprocessing

1. Place the input files in the same folder.
2. Run noteEvents_preproc.py script with input (NOTEEVENTS.csv). It will produce the output file (output.csv)
It took approximately 2 hours on AWS Elastic Compute Cloud (EC2) instance with a c5.12xlarge instance type.
```
python3 noteEvents_preproc.py NOTEEVENTS.csv &  
```
3. Run MIMIC_smart_splitter.py (with output.csv as input): splits the preprocessed text into files of 50 Mb without cutting any notes - it took approx. 15 mins.
```
python3 MIMIC_smart_splitter.py output.csv &  
```
4. At this step, we have a new folder called "data," which contains two folders. The first one (chunkssmall) contains all files, and the other one is empty.

## CUI Recognizer with QuickUMLS (concept extraction)

Reference: [UMLS installation](https://github.com/Georgetown-IR-Lab/QuickUMLS/blob/master/README.md)

## Models Training and Validation

Due to license constraints, we have not uploaded the data sets on the GitHub link. 

```
nohup python3 02_FFN_diagprediction.py --nEpochs 100 --withCCS 0 > org_withccs_epochs100.log &
nohup python3 02_FFN_diagprediction.py --nEpochs 100 --withCCS 1 > org_withoutccs_epochs100.log &
nohup python3 02_FFN_diagprediction.py --nEpochs 100 --withCCS 0  --lr 0.03 > org_withccs_epochs100_lr3.log &
nohup python3 02_FFN_diagprediction.py --nEpochs 100 --withCCS 0  --lr 0.03 --dropOut 0.7 > org_withccs_epochs100_lr3_dropout07.log &

nohup python3 02_FFN_diagprediction_modified.py --nEpochs 100 --withCCS 0 > mod_withccs_epochs100.log &
nohup python3 02_FFN_diagprediction_modified.py --nEpochs 100 --withCCS 1 > mod_withoutccs_epochs100.log &
nohup python3 02_FFN_diagprediction_modified.py --nEpochs 100 --withCCS 0  --lr 0.03 > mod_withccs_epochs100_lr3.log &
nohup python3 02_FFN_diagprediction_modified.py --nEpochs 100 --withCCS 0  --lr 0.03 --dropOut 0.7 > mod_withccs_epochs100_lr3_dropout07.log &

```

## Results

![Alt Text](result_image/results.png)
