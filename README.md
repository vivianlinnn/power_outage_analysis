# Outage Analysis Project
Fall '24 DSC 80 Project 

**By:** Vivian Lin, Selina Zhang


## Introduction
This project revolves around a dataset that provides rich information about power outages across the states, including time, location, climate conditions, and urbanization levels. We can use this dataset to identify patterns of power outages to infer problems of these outages. The main question is **where are the causes of major outages?** Readers of our website should care because we use electricity to make everything easier for our lives such as lights, various machinaries, and the internet. Thus, analyzing power outages can help us better prepare when and where to expect power outages. 

The dataset comprises of 1534 rows.

These are the columns we used:

| **Column Name**       | **Description**                                                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `YEAR`                | Year when the outage event occurred.                                                                                                                                             |
| `MONTH`               | Month when the outage event occurred.                                                                                                                                            |
| `NERC.REGION`         | The North American Electric Reliability Corporation (NERC) regions impacted by the outage event.                                                                               |
| `CLIMATE.REGION`      | U.S. Climate regions as specified by the National Centers for Environmental Information.                                                                                         |
| `CLIMATE.CATEGORY`    | Represents the climate episodes corresponding to the years. The categories are “Warm”, “Cold”, or “Normal”.                                                                    |
| `CAUSE.CATEGORY`      | Categories of events causing the major power outages (e.g., weather-related, equipment failure, human error, etc.).                                                             |
| `OUTAGE.DURATION`     | Duration of the outage event (measured in hours, days, etc.).                                                                                                                  |
| `CUSTOMERS.AFFECTED`  | Number of customers affected by the power outage event.                                                                                                                        |
| `RES.PERCEN`          | Percentage of residential electricity consumption compared to the total electricity consumption in the state (in %).                                                          |
| `ANOMALY.LEVEL`       | Represents the oceanic El Niño/La Niña (ONI) index referring to cold and warm episodes by season. It is estimated as a 3-month running mean of ERSST.v4 SST anomalies in the Niño 3.4 region (5°N to 5°S, 120–170°W). |
| `TOTAL.REALGSP`       | Real Gross State Product (GSP) contributed by all industries (total), measured in 2009 chained U.S. dollars.                                                                  |
| `DEMAND.LOSS.MW`      | Amount of peak demand lost during an outage event (in Megawatts). In many cases, total demand is reported as the description.                                                  |



## Data Cleaning and Exploratory Data Analysis

### Dataset

| **YEAR** | **MONTH** | **NERC.REGION** | **CLIMATE.REGION** | **CLIMATE.CATEGORY** | **CAUSE.CATEGORY**  | **OUTAGE.DURATION** | **CUSTOMERS.AFFECTED** | **RES.PERCEN** | **ANOMALY.LEVEL** | **TOTAL.REALGSP** | **DEMAND.LOSS.MW** |
|----------|-----------|-----------------|--------------------|----------------------|---------------------|---------------------|-----------------------|----------------|-------------------|-------------------|---------------------|
| 2011     | 7         | MRO             | East North Central | normal               | severe weather      | 3060                | 70000                 | 35.549073       | -0.3              | 274182            | NaN                 |
| 2014     | 5         | MRO             | East North Central | normal               | intentional attack  | 1                   | NaN                   | 30.032487       | -0.1              | 291955            | NaN                 |
| 2010     | 10        | MRO             | East North Central | cold                 | severe weather      | 3000                | 70000                 | 28.097672       | -1.5              | 267895            | NaN                 |
| 2012     | 6         | MRO             | East North Central | normal               | severe weather      | 2550                | 68200                 | 31.994099       | -0.1              | 277627            | NaN                 |
| 2015     | 7         | MRO             | East North Central | warm                 | severe weather      | 1740                | 250000                | 33.982576       | 1.2               | 292023            | 250                 |


## Assessment of Missingness
NMAR Column: OUTAGE.RESTORATION.TIME, because the likelihood of the restoration time itself, longer outages are less likely to be reported, outages might have not ended it or they might not have the advanced infrastructure to report the data so there are more bias towards areas with the kind of infrastruction to report the data of the end data of the restoration time.

MAR Column: Reject the null, the misssingness of CAUSE.CATEGORY.DETAIL is dependent on CLIMATE.REGION
For CAUSE.CATEGORY.DETAIL on YEAR column, fail to reject the null, CAUSE.CATEGORY.DETAIL not dependent on year

### Missingness Dependency

**Null Hypothesis:** The missingness of `CUSTOMERS.AFFECTED` is independent of the column `CLIMATE.CATEGORY`. 

**Alternative Hypothesis:** The missingness of `CUSTOMERS.AFFECTED` is dependent of the column `CLIMATE.CATEGORY`.

**Test Statistic:** TVD

<img width="1079" alt="image" src="https://github.com/user-attachments/assets/d5ac2a86-0bed-4a4b-a338-9fd82d142f70">
Our p-value of 0.753 is greater than our significance level of 0.05, meaning we fail to reject the null hypothesis. We conclude that the missingness of `CUSTOMERS.AFFECTED` is not significantly associated with the column` CLIMATE.CATEGORY `and is independent on `CLIMATE.CATEGORY`. 

## Hypothesis Testing


## Framing a Prediction Problem
Our Prediction Problem: We decided to use classification to do a binary classifer to predict the column 'CLIMATE.REGION' because we think it answers our central question: "Where does outages occur"

## Baseline Model

## Final Model

## Fairness Analysis
