# International Validity of US Trained Demographic Classifiers

This repository contains the notebooks and resources for our manuscript "Lost In Translation: Limitations of Deep Learning Demographic Classification Models Developed on US Imaging Datasets In Global Contexts". Specifically, this repository contains the training and validation notebooks for Deep Learning models trained to classify demographic variables (age, sex, race) on the MIMIC, NIH, and CheXpert publicly available US datasets. In addition, it holds the notebooks used to assess the performance of these US dataset-trrained models on internationally sourced datasets. The notebooks were developed and deployed in Google Colab from 2022-2025 using the default Python version at the time, with standard scientific libraries (e.g., numpy, matplotlib, pandas). AI models were developed using the fast.ai library in 2022 with the default Google Colab installation at the time (version 2.7.7). There are no specific installation guides, as these notebooks are intended to help users understand our workflow and logic in the spirit of literate programming. In a Google Colab environment, the notebooks will run succesfully when given the appropriate file names and paths, and will generate the appropriate PKL, CSV and figure outputs as specified.

# Data Availability
This study utilizes ten publicly available chest X-ray datasets. The CheXpert dataset can be accessed at https://stanfordmlgroup.github.io/competitions/chexpert/. Similarly, the MIMIC-CXR dataset can be obtained through PhysioNet at https://physionet.org/content/mimic-cxr/2.0.0/. Information on patient race and ethnicity can be found in the admissions.csv file within the MIMIC-IV dataset at https://physionet.org/content/mimiciv. The final US dataset, NIH Chest X-ray dataset, is hosted on Kaggle at https://www.kaggle.com/datasets/nih-chest-xrays/data.

The BRAX dataset can be accessed via PhysioNet at https://physionet.org/content/brax/1.1.0/, while the PadChest dataset is available through the BIMCV platform https://bimcv.cipf.es/bimcv-projects/padchest/. The JSRT dataset can be accessed either through http://db.jsrt.or.jp/eng.php or its Kaggle mirror at https://www.kaggle.com/datasets/raddar/nodules-in-chest-xrays-jsrt. The Shenzhen TB dataset is available of Kaggle as well at https://www.kaggle.com/datasets/raddar/tuberculosis-chest-xrays-shenzhen. Additionally, the VinDr dataset and its pediatric counterpart, VinDr-PCXR, are both hosted on PhysioNet at https://physionet.org/content/vindr-cxr/1.0.0/ and https://physionet.org/content/vindr-pcxr/1.0.0/, respectively. Finally, the India TB dataset can be accessed through https://sourceforge.net/projects/tbxpredict/. Each of these datasets has specific data use agreements, credentialing requirements, and usage guidelines, all of which are detailed on their respective hosting sites.



<img width="4200" height="3300" alt="Copy of Int_Validity_Pipeline" src="https://github.com/user-attachments/assets/45e9e30c-e588-4220-8523-280ff04b99be" />

# Model Training
The dataset splits and model training code for the MIMIC and CheXpert-trained models can be found in the CheXpert_Model_Train, MIMIC_Model_Train, and NIH_Model_Train  folders. The labeling schemes were based on the work of Seyyed-Kalantari et al.* and Gichoya et al.** Each dataset was divided into a 70/10/20 train-validation-test split for each demographic variable (race, age, sex). A separate ResNet34 classification model was trained for each variable within each dataset. As the NIH dataset, did not contain race labels, a race classifying model was not developed from this dataset. Trained model weights were stored in PKL files and the dataset splits were stored in CSV files. A total of 3 age classifiers, 3 sex classifiers, and 2 race classifiers were developed. 

# Model Testing
The trained models were evaluated using three U.S.-based datasets: CheXpert (Palo Alto, CA), MIMIC-CXR (Boston, MA), and NIH ChestX-ray14 (Bethesda, MD). To assess generalizability, the models were further validated on six international datasets. These include BRAX from Brazil (South America), PadChest from Spain (Europe), and five datasets from Asia: VinDr and VinDr-PCXR (Vietnam), JSTR (Japan), Shenzhen Tuberculosis (China), and India Tuberculosis (India).

Among all datasets, only MIMIC-CXR and CheXpert include self-reported race labels. For these two datasets, the analysis focused on four well-represented race categories: Hispanic/Latino, Asian, Black, and White. For international datasets that did not provide race annotations, race and ethnicity were inferred based on the country of origin, using U.S. Census definitions. Specifically, patients from Asian countries were classified as Asian, those from South America as Hispanic/Latino, and those from Europe as White.

Since the U.S.-based datasets were used for model training, the held-out test sets from their respective train-validation-test splits were used to evaluate model performance. In contrast, because the international (non-U.S.) datasets were not used during training, their full datasets were used for model evaluation.

Model testing scripts are located in the Model_Testing directory, which is divided into three subfolders: Age_Testing, Race_Testing, and Sex_Testing. Each folder contains a set of Jupyter notebooks named according to the dataset and demographic variable being evaluated. For example, brax_age_validation.ipynb is a notebook in which the BRAX dataset is used to validate the three age classification models. The results of model performance evaluations are stored in CSV files within these directories.

# Data Analysis and Visualization
Model performance was evaluated differently depending on the composition of the test dataset. For datasets with heterogeneous distributions of demographic labels (i.e., those containing individuals from multiple age, sex, or race groups) performance was assessed using the area under the receiver operating characteristic curve (AUC) following a one-vs-all classification strategy. To summarize overall performance within each demographic category, we computed the weighted average AUC (wAUC) and weighted average precision score. Each score was weighted by the prevalence of the corresponding label in the test set.

In contrast, for datasets that were homogeneous with respect to a given demographic variable, such as the VinDr-PCXR dataset, where all individuals fell within the 0–20 years age group, performance was reported using predictive accuracy instead of AUC.

To better quantify uncertainty and assess the robustness of the models, 95% confidence intervals were calculated for both wAUC and weighted average precision using bootstrap resampling.

The notebooks used to analyze results from model testing are located in the Analysis_Scripts directory. Each notebook is named to indicate which demographic classifier is being evaluated. These notebooks ingest the .csv files produced by the model testing scripts and compute the wAUC and weighted average precision along with 95% bootstrap confidence intervals.

In the Visualization folder, the provided notebooks generate barplots for the wAUC and associated 95% CI for each demographic classification task.

# Terminology Notes
In our documentation, we sometimes use the terms gender and sex interchangeably, though they are distinct concepts. Similarly, race and ethnicity may be conflated at times. This is due to differences in how these categories were recorded in publicly available datasets. Age categories are defined as follows: 0 → 0-20 years old; 1 → 21-40 years old; 2 → 41-60 years old; 3 → 61-80 years old; 4 → 81+ years old.


*Seyyed-Kalantari L, Zhang H, McDermott MBA, Chen IY, Ghassemi M. Underdiagnosis bias of artificial intelligence algorithms applied to chest radiographs in under-served patient populations. Nat Med. 2021;27(12):2176-2182. doi:10.1038/s41591-021-01595-0 
**Gichoya JW, Banerjee I, Bhimireddy AR, et al. AI recognition of patient race in medical imaging: a modelling study. Lancet Digit Health. 2022;4(6):e406-e414. doi:10.1016/S2589-7500(22)00063-2
