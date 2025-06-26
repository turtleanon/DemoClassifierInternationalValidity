# International Validity of US Trained Demographic Classifiers

This repository contains the notebooks and resources for our manuscript "Trained in America, Confused Abroad? Limitations of Deep Learning Demographic Classifying Models Developed on U.S. Imaging Datasets". Specifically, this repository contains the training and validation notebooks for Deep Learning models trained to classify demographic variables (age, sex, race) on the MIMIC, NIH, and CheXpert publicly available US datasets. In addition, it holds the notebooks used to assess the performance of these US dataset-trrained models on internationally sourced datasets. The notebooks were developed and deployed in Google Colab from 2022-2024 using the default Python version at the time, with standard scientific libraries (e.g., numpy, matplotlib, pandas). AI models were developed using the fast.ai library in 2022 with the default Google Colab installation at the time (version 2.7.7). There are no specific installation guides, as these notebooks are intended to help users understand our workflow and logic in the spirit of literate programming. In a Google Colab environment, the notebooks will run succesfully when given the appropriate file names and paths, and will generate the appropriate PKL, CSV and figure outputs as specified.

# Data Availability

![image](https://github.com/user-attachments/assets/655467fb-dde6-41ae-aff7-ed10fe137f9d)
# Model Training

# Model Testing

# Data Analysis and Visualization

# Terminology Notes
In our documentation, we sometimes use the terms gender and sex interchangeably, though they are distinct concepts. Similarly, race and ethnicity may be conflated at times. This is due to differences in how these categories were recorded in publicly available datasets. Age categories are defined as follows: 0 → 0-20 years old; 1 → 21-40 years old; 2 → 41-60 years old; 3 → 61-80 years old; 4 → 81+ years old.
