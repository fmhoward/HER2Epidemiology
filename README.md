# Epidemiology and Prognosis of HER2-Low Breast Cancer in the National Cancer Data Base
Code to compute the epidemiology and prognosis of HER2-low breast cancer in NCDB
<br>
<img src="https://github.com/fmhoward/HER2Epidemiology/blob/main/Figure 1.png?raw=true" width="600">

## Attribution
If you use this code in your work or find it helpful, please consider citing our work in <a href='https://doi.org/10.1001/jamaoncol.2022.7476'>JAMA Oncology</a>.
```
@article{peiffer_clinicopathologic_2023,
	title = {Clinicopathologic {Characteristics} and {Prognosis} of {ERBB2}-{Low} {Breast} {Cancer} {Among} {Patients} in the {National} {Cancer} {Database}},
	issn = {2374-2437},
	url = {https://doi.org/10.1001/jamaoncol.2022.7476},
	doi = {10.1001/jamaoncol.2022.7476},
	abstract = {Given conflicting results regarding the prognosis of erb-b2 receptor tyrosine kinase 2 (ERBB2; formerly HER2 or HER2/neu)–low breast cancer, a large-scale, nationally applicable comparison of ERBB2-low vs ERBB2-negative breast cancer is needed.To investigate whether ERBB2-low breast cancer is a clinically distinct subtype in terms of epidemiological characteristics, prognosis, and response to neoadjuvant chemotherapy.This retrospective cohort study was conducted using the National Cancer Database, including 1 136 016 patients in the US diagnosed with invasive breast cancer from January 1, 2010, to December 31, 2019, who had ERBB2-negative disease and had immunohistochemistry results available. ERBB2-low tumors were classified as having an immunohistochemistry score of 1+, or 2+ with a negative in situ hybridization test. Data were analyzed from November 1, 2021, through November 30, 2022.Standard therapy according to routine clinical practice.The primary outcomes were overall survival (OS), reported as adjusted hazard ratios (aHRs), and pathologic complete response, reported as adjusted odds ratios (aORs), for ERBB2-negative vs ERBB2-low breast cancer, controlling for age, sex, race and ethnicity, Charlson-Deyo Comorbidity Index score, treatment facility type, tumor grade, tumor histology, hormone receptor status, and cancer stage.The study identified 1 136 016 patients (mean [SD] age, 62.4 [13.1] years; 99.1\% female; 78.6\% non-Hispanic White), of whom 392 246 (34.5\%) were diagnosed with ERBB2-negative and 743 770 (65.5\%) with ERBB2-low breast cancer. The mean (SD) age of the ERBB2-negative group was 62.1 (13.2) years and 62.5 (13.0) years for the ERBB2-low group. Higher estrogen receptor expression was associated with increased rates of ERBB2-low disease (aOR, 1.15 per 10\% increase). Compared with non-Hispanic White patients, of whom 66.1\% were diagnosed with ERBB2-low breast cancer, fewer non-Hispanic Black (62.8\%) and Hispanic (61.0\%) patients had ERBB2-low disease, although in non-Hispanic Black patients this was mediated by differences in rates of triple-negative disease and other confounders. A slightly lower rate of pathologic complete response was seen in patients with ERBB2-low disease vs patients with ERBB2-negative disease on multivariable analysis (aOR, 0.89; 95\% CI, 0.86-0.92; P \&lt; .001). ERBB2-low status was also associated with small improvements in OS for stage III (aHR, 0.92; 95\% CI, 0.89-0.96; P \&lt; .001) and stage IV (aHR, 0.91; 95\% CI, 0.87-0.96; P \&lt; .001) triple-negative breast cancer, although this amounted to only a 2.0\% (stage III) and 0.4\% (stage IV) increase in 5-year OS.This large-scale retrospective cohort analysis found minimal prognostic differences between ERBB2-low and ERBB2-negative breast cancer. These findings suggest that, moving forward, outcomes in ERBB2-low breast cancer will be driven by ERBB2-directed antibody-drug conjugates, rather than intrinsic differences in biological characteristics associated with low-level ERBB2 expression. These findings do not support the classification of ERBB2-low breast cancer as a unique disease entity.},
	urldate = {2023-04-17},
	journal = {JAMA Oncology},
	author = {Peiffer, Daniel S. and Zhao, Fangyuan and Chen, Nan and Hahn, Olwen M. and Nanda, Rita and Olopade, Olufunmilayo I. and Huo, Dezheng and Howard, Frederick M.},
	month = feb,
	year = {2023},
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
