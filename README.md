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

## Misclassification
There have been <a href='https://pubmed.ncbi.nlm.nih.gov/35113160/'>several studies</a> suggesting that classification of HER2-low versus HER2-0 via IHC is inconsistent. This may have reduced the magnitude of associations of HER2-low status with outcomes in our findings. We can estimate the impact of misclassification (i.e. error rate, or sum of false positive and false negative classification of HER2-low status) on our results as follows.

We take for example, the association we found of HER2-low status with lower rates of pathologic complete response to neoadjuvant chemotherapy. We use this as an example because the magnitude of the association was among the highest seen for our study, so the impact of misclassification on other outcomes is almost certainly lower. Additionally, adjusting for misclassification mathematically for odds ratios is easier than for survival models.

We construct a contigency table approximating the association of HER2-low status with pathologic complete response (after adjustment for other factors); i.e. assuming approximately 35% of patients are HER2-0, approximately 20% of patients had a complete response, and the odds ratio for HER2-low status with complete response is 0.89:
```
		pCR	Residual Disease	Total
HER2-0		7.4	27.6			35
HER2-Low	12.6	52.4			65
Total		20	80			100
```

We then assume there is an equal misclassification rate among both HER2-Low and HER2-0 patients, and that the overall number of patients misclassified is x. We can then define the rates of pathologic complete response among true HER2-0 and true HER2-low patients, along with an updated contigency table:

```
True HER2-0 pCR Rate = a = (7.4 + 0.65 * a * x - 0.35 * b * x)/(35 + 0.65 * x - 0.35 * x)
True HER2-Low pCR Rate = b = (12.6 - 0.65 * a * x + 0.35 * b * x)/(65 + 0.35 * x - 0.65 * x) 

		pCR					Residual Disease					Total
HER2-0		7.4 + 0.65 * a * x - 0.35 * b * x	27.6 + 0.65 * (1 - a) * x - 0.35 * (1 - b) * x		35 + 0.3 * x
HER2-Low	12.6 - 0.65 * a * x + 0.35 * b * x	52.4 - 0.65 * (1 - a) * x + 0.35 * (1 - b) * x		65 - 0.3 * x
Total		20					80							100
```

We can plot the resulting odds ratio as a function of the misclassification rate x, ranging from 0 (indicating the current classification was perfect) to 50 (indicating that classification of HER2-0 and HER2-low is occuring at random). Of note, a misclassification of > 50% would indicate anti-correlation of HER2-IHC and true underlying HER2 expression:

<img src="https://github.com/fmhoward/HER2Epidemiology/blob/main/misclassification.png?raw=true" width="600">

Thus, a misclassfiication rate of over 28% is required to double the effect size of HER2-low status on rates of pathologic complete response, and this effect size would still be fairly marginal (equivalent to a ~20% change in hormone receptor status expression). The true misclassification rate of HER IHC is unknown, given the lack of a gold standard of low level HER2 expression. However, we can attempt to estimate rates of misclassification from published work. <a href='https://pubmed.ncbi.nlm.nih.gov/35113160/'>A prior study</a> assessed concordance between 18 pathologists in classifying 170 cases ranging from HER2-0 to HER2-3+ by IHC, and found there was significant variability in the classiifcation of cases as HER2-Low versus HER2-0. We can create an optimistic lower bound of the misclassification rate suggested by this study, by assuming that the cases for which a majority of pathologists classified as HER2-Low are truly HER2-Low, and the cases for which a majority of pathologists classified as HER2-0 are truly HER2-0.

<img src="https://github.com/fmhoward/HER2Epidemiology/blob/main/optimistic4.png?raw=true" width="600">

Using analysis of pixel areas, we can reconstruct an approximate representation of the pathologist grading of samples from this study, using an estimation of the midpoint of HER2 3+ to remove samples that would be HER2 3+ from the analysis (as these are not relevant for the distinction of HER2-0 and HER2-Low).

| Readers     | HER2 0 | HER2 1-2+ |
|-------------|--------|-----------|
| 1           | 23     | 116       |
| 2           | 24     | 115       |
| 3           | 26     | 113       |
| 4           | 29     | 110       |
| 5           | 29     | 110       |
| 6           | 31     | 108       |
| 7           | 33     | 106       |
| 8           | 37     | 102       |
| 9           | 40     | 99        |
| 10          | 42     | 97        |
| 11          | 44     | 95        |
| 12          | 44     | 95        |
| 13          | 47     | 92        |
| 14          | 52     | 87        |
| 15          | 54     | 85        |
| 16          | 61     | 78        |
| 17          | 78     | 61        |
| 18          | 92     | 47        |

Using this data, we can determine that approximately 10% of cases would be misclassified in an optimistic projection (where the minority class is the misclassified group), with a false positive rate for HER2-Low of 5% and a false negative rate of 20%. This would result in a reduction in the odds ratio to 0.87. 

In reality, some of the cases deemed 'HER2-Low' by the majority may actually be HER2-0, and vice versa, so the true misclassification rate is slightly higher. We can perform a more realistic projection by assuming that any case with over 20% disagreement is equally like to be 'true' HER2-0 or 'true' HER2-Low, which slightly increases the FPR to 8% and FNR to 22% (overall misclassification of 14%), and odds ratio of 0.86. A 20% disagremeent was chosen for this projection as the likelihood of misclassification when agreement is seen in 15/18 raters with a false positive rate of ~20% is < 0.01%. 

<img src="https://github.com/fmhoward/HER2Epidemiology/blob/main/realistic.png?raw=true" width="600">

Calculating an exact rate of misclassification when no gold standard is known is not straightforward, and relies on a variety of assumptions. There is almost certainly disagreement between HER2 mRNA expression, protein expression, and automated techniques to immunohistochemistry interpretation, and the misclassification of HER2 IHC interpreted by pathologists could be inflated by chosing an alternative 'gold standard' that is most dissimilar to IHC. However, these estimates of misclassification can be used to account for errors due to inter-observer variability, and it is clear that half or more of cases are uniformly and consistently classified by large numbers of pathologists. As we can see, when accounting for misclassification, the these minor differences in outcome do not support the classification of HER2-Low disease as a unique prognostic entity prior to the introduction of antibody drug conjugates for this population.




