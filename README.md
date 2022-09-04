# Epidemiology and Prognosis of HER2-Low Breast Cancer in the National Cancer Data Base
Code to compute the epidemiology and prognosis of HER2-low breast cancer in NCDB
<br>
<img src="https://github.com/fmhoward/HER2Epidemiology/blob/main/Figure 1.png?raw=true" width="600">

## Attribution
If you use this code in your work or find it helpful, please consider citing our work.
```
@article {
	author = {Peiffer, Daniel and Zhao, Fangyuan and Chen, Nan and Nanda, Rita and and Olopade, Olufunmilayo I. and Huo, Dezheng and Howard, Frederick Matthew},
	title = {Epidemiology and Prognosis of HER2-Low Breast Cancer in the National Cancer Data Base},
	year = {2022},
	abstract = {Importance: Given conflicting results from retrospective cohort studies regarding the prognosis of HER2-low breast cancer, a large-scale, nationally applicable, comparison of HER2-low vs. HER2-0 breast cancer is needed. 
Objective: To investigate whether HER2-low breast cancer is a clinically distinct subtype with a unique epidemiology, prognosis, and response to neoadjuvant chemotherapy.
Design/Participants/Setting: A retrospective cohort analysis was conducted using the National Cancer Database, including 1,136,016 patients with invasive breast cancer nationally from 2010 to 2019 that were HER2 negative and had immunohistochemistry results available. HER2-low tumors were classified as immunohistochemistry score of 1+, or 2+ with a negative in-situ hybridization test. Data were analyzed from November 2021 through June 2022.
Exposures: Standard therapy according to routine clinical practice.
Main Outcomes and Measures: Hazard ratio for overall survival and odds ratio for pathologic complete response for HER2-0 versus HER2-low breast cancer, controlling for age, race/ethnicity, comorbidity index, treatment facility type, tumor grade, histologic subtype, receptor status, and stage.
Results: We identified n = 392,246 patients with HER2-0 and n = 743,770 patients with HER2-low disease for analysis. Compared to non-Hispanic White patients where 66.1% of cases were HER2-low, fewer non-Hispanic Black (62.8%) and Hispanic (61.0%) patients were HER2-low, although this is largely mediated by differences in rates of triple-negative disease and other confounders. On multivariable analysis, HER2-low status was associated with longer overall survival (OS) for stage II (hazard ratio [HR] 0.94, 95% CI 0.91 – 0.97, p < 0.01), stage III (HR 0.92, 0.88 – 0.96, p < 0.01) and stage IV (HR 0.93, 0.88 – 0.98, p = 0.01) triple-negative breast cancer and in stage IV (HR 0.95, 0.92 – 0.99, p < 0.01) hormone receptor positive breast cancer. Analysis of 84,440 patients that received neoadjuvant chemotherapy demonstrated lower complete pathological response in HER2-low disease on multivariable analysis (adjusted odds ratio [OR] 0.87, 95% CI 0.84 - 0.90, p < 0.01).
Conclusions and Relevance: This large-scale retrospective analysis suggests HER2-low breast cancer represents a distinct clinical subset associated with an improved prognosis, but lower rates of response to chemotherapy, highlighting the utility of targeted therapies for this subset of patients.},
	URL = {https://github.com/fmhoward/HER2Epidemiology},
}

```

## Installation
The attached python notebook can be downloaded and run from Jupyter. Installation takes < 5 minutes on a standard desktop computer. Runtime for all code is approximately 5 minutes. All software was tested on Windows 11 with a Intel(R) Core(TM) i5-10210U CPU.

Requirements:
* python 3.7.5
* statsmodels 0.13.2
* lifelines 0.27.1
* pandas 1.3.5
* numpy 1.21.2

## Overview
Place the NCDB 2019 data file in csv form within the project folder, and specify the location of the csv file in the following line under 'Loading the NCDB File' header. Subsequently, all cells can be run within the notebook to replicate the results of the study.
```
df = load_data_her2(filename="NCDBPUF_Breast.0.2019.csv", savefile="NCDB_Subset.csv", lower=True)
```
