# cs598_dlh_patient_trajectory_prediction

## The original GitHub repository
[JamilProg/patient_trajectory_prediction](https://github.com/JamilProg/patient_trajectory_prediction/blob/master/README.md)

## Download the data from MIMIC III data

We are using the MIMIC III data. We have requested access to data by following the mandatory training. After getting the approval, we downloaded the required files. This paper only needed the below subset of files:
NOTEEVENTS.csv
ADMISSIONS.csv
DIAGNOSES_ICD.csv


## Install the required packages
`python3 -m venv venv`
`source venv/bin/activate`
`pip install -r requirements.txt`

## Data Preprocessing

1. Place the input files in the same folder.
2. Run noteEvents_preproc.py script with input (NOTEEVENTS.csv). It will produce the output file (output.csv)
It took approximately 2 hours on AWS Elastic Compute Cloud (EC2) instance with a c5.12xlarge instance type.
3. Run MIMIC_smart_splitter.py (with output.csv as input): splits the preprocessed text into files of 50 Mb without cutting any notes - it took approx. 15 mins.
4. At this step, we have a new folder called "data," which contains two folders. The first one (chunkssmall) contains all files, and the other one is empty.

## CUI Recognizer with QuickUMLS (concept extraction)

Note: Obtain a UMLS installation This tool requires you to have a valid UMLS installation on disk. To install UMLS, you must first obtain a license from the National Library of Medicine; then you should download all UMLS files from this page; finally, you can install UMLS using the MetamorphoSys tool as explained in this guide. The installation can be removed once the system has been initialized.
Reference: [UMLS installation](https://github.com/Georgetown-IR-Lab/QuickUMLS/blob/master/README.md)

**We requested a license on April 15, 2023. It may take three business days.**

