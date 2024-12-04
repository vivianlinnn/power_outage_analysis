# Title: Outage Analysis Project

**Name(s)**: Vivian Lin, Selina Zhang



## Introduction

## Data Cleaning and Exploratory Data Analysis

## Assessment of Missingness
NMAR Column: OUTAGE.RESTORATION.TIME, because the likelihood of the restoration time itself, longer outages are less likely to be reported, outages might have not ended it or they might not have the advanced infrastructure to report the data so there are more bias towards areas with the kind of infrastruction to report the data of the end data of the restoration time.

MAR Column: Reject the null, the misssingness of CAUSE.CATEGORY.DETAIL is dependent on CLIMATE.REGION
For CAUSE.CATEGORY.DETAIL on YEAR column, fail to reject the null, CAUSE.CATEGORY.DETAIL not dependent on year


## Hypothesis Testing
**Null Hypothesis:** The missingness of `CUSTOMERS.AFFECTED` is independent of the column `CLIMATE.CATEGORY`. 

**Alternative Hypothesis:** The missingness of `CUSTOMERS.AFFECTED` is dependent of the column `CLIMATE.CATEGORY`.

We chose to use the TVD to predict the column 'CLIMATE.CATEGORY'
<img width="1079" alt="image" src="https://github.com/user-attachments/assets/d5ac2a86-0bed-4a4b-a338-9fd82d142f70">
We achieved a p-value of 0.778, which is greater than the observed statistic 0.05, thus, we rejected the null hypothesis

## Framing a Prediction Problem
Our Prediction Problem: We decided to use classification to do a binary classifer to predict the column 'CLIMATE.REGION' because we think it answers our central question: "Where does outages occur"

## Baseline Model

## Final Model

## Fairness Analysis
