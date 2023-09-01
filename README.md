# ML_Atc_DT_PFX
Repository for "Drug target, class level, and PathFX pathway information share utility for machine learning prediction of common drug-induced side effects" by Han Jie Liu & Jennifer L. Wilson...


**main_code.ipynb** is the Python script we wrote to execute this project

**Below is a list of link to the resources and datasets used from them to generate project results
**1. http://sideeffects.embl.de/download/
   a. meddra_all_se.tsv: contains all drug to side effect combinations curated in SIDER 4.1 based on MedDRA classification
   b. drug_names.tsv: dataset containing all drug names and its unique drug ID in SIDER 4.1
2. https://github.com/jenwilson521/PathFX/blob/master/rscs/Pfx050120_dint.pkl: consists of a pickled dictionary of all drugbank drugs with its associated targets
3. https://go.drugbank.com/releases/latest#open-data
   a. drugbank_vocabulary.csv: a curated list of all common names and synonyms associated with drugs in DrugBank
4. https://go.drugbank.com/releases
   a. DrugBank release version 5.1.6


**Below is a list of excel files along with a brief description of the tabs associated with each excel file
**1.	Characteristics.xlsx:
  a.	data characteristics: contains 1) total count of side effects, 2) number of drugs associated with side effect, 3) number of drugs matched to DBID, 4) DBID match %, 5) matrix match count and 6) matrix match %
  b.	LR vs RFC: comparison of LR and RFC model prediction across 30 side effects with 100x bootstrap with random undersample of negative cases
  c.	average accuracy across 5 conditions: average accuracy of model performance for prediction of 30 side effects in 1) ATC model, 2) DT model, 3) DT/PathFX model, 4) DT/ATC model, and 5) DT/PathFX/ATC model
  d.	ANOVA-RM: repeated measures ANOVA across the 5 conditions sorted based on the highest to lowest prediction accuracy from the DT model

2.	LR_Coefficients.xlsx:
  a.	experimental drug target coefficients: count of the 10 most common unapproved drug target with its assigned LR coefficients across 30 side effects trained on the unfiltered dataset
  b.	gastrointestinal disorder: top and bottom 30 LR coefficients for this side effect
  c.	hypersensitivity: top and bottom 30 LR coefficients for this side effect
  d.	dermatitis: top and bottom 30 LR coefficients for this side effect

3.	all_ttest_results.xlsx:
  a.	DT vs DT/PathFX: paired t-test table comparing the performance of DT vs DT/PathFX model
  b.	DT/ATC vs DT/ATC/PathFX: paired t-test table comparing the performance of DT/ATC vs DT/ATC/PathFX model
  c.	ATC effects: 3 paired t-test tables comparing the performance of: 1) ATC vs DT model, 2) DT vs DT/ATC model, and 3) DT/PathFX vs DT/ATC/PathFX model



