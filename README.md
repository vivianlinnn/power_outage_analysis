# <span style="color: green;"> Power Outage Analysis <\span>
Fall '24 DSC 80 Project 

**By:** Vivian Lin, Selina Zhang


## Introduction
This project revolves around a dataset that provides rich information about power outages across the states, including time, location, climate conditions, and urbanization levels. We can use this dataset to identify patterns of power outages to infer problems of these outages. The main question is **where are the causes of major outages?** Readers of our website should care because we use electricity to make everything easier for our lives such as lights, various machinaries, and the internet. Thus, analyzing power outages can help us better prepare for where outages are more likely to happen and where do dedicate more resources to the regions where more people are affected. 

The dataset comprises of 1534 rows.

Although there is a total of 57 columns, we are only going to use the ones below:

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

We cleaned the data set by just extracting the relevent columns of `YEAR`, `MONTH`, `NERC.REGION`, `CLIMATE.REGION`, `CLIMATE.CATEGORY`, `CAUSE.CATEGORY`, `OUTAGE.DURATION` , `CUSTOMERS.AFFECTED`, `RES.PERCEN`, `ANOMALY.LEVEL`, and `DEMAND.LOSS.MW`.

Although we did not initially make any new columns in this step, we made copies of this original dataframe and added necessary columns for those particular steps. 

### First 5 Rows of Dataset

| **YEAR** | **MONTH** | **NERC.REGION** | **CLIMATE.REGION** | **CLIMATE.CATEGORY** | **CAUSE.CATEGORY**  | **OUTAGE.DURATION** | **CUSTOMERS.AFFECTED** | **RES.PERCEN** | **ANOMALY.LEVEL** | **TOTAL.REALGSP** | **DEMAND.LOSS.MW** |
|----------|-----------|-----------------|--------------------|----------------------|---------------------|---------------------|-----------------------|----------------|-------------------|-------------------|---------------------|
| 2011     | 7         | MRO             | East North Central | normal               | severe weather      | 3060                | 70000                 | 35.549073       | -0.3              | 274182            | NaN                 |
| 2014     | 5         | MRO             | East North Central | normal               | intentional attack  | 1                   | NaN                   | 30.032487       | -0.1              | 291955            | NaN                 |
| 2010     | 10        | MRO             | East North Central | cold                 | severe weather      | 3000                | 70000                 | 28.097672       | -1.5              | 267895            | NaN                 |
| 2012     | 6         | MRO             | East North Central | normal               | severe weather      | 2550                | 68200                 | 31.994099       | -0.1              | 277627            | NaN                 |
| 2015     | 7         | MRO             | East North Central | warm                 | severe weather      | 1740                | 250000                | 33.982576       | 1.2               | 292023            | 250                 |

### Univariate Analyses
When performing univariate analyses, we observe for the distribution of single variables.

#### Distribution of Outages in Different Climate Regions
<img width="1079" alt="image" src="climate_region_counts.jpg">
As observed, the greatest number of outages reported in the years 2000 to 2016 are the Northeast and South regions.


#### Distribution of Outages Across Different Months of the Year
<img width="1079" alt="image" src="month_counts.jpg">
As observed, outages are reported in the largest numbers in the months of June, July, and August. These months are in the season of summer, therefore according to the graph, outages are more likely to happen in the summer.


### Bivariate Analyses
When performing bivariate analyses, we observe for the relationship of two variables.

#### Climate Region vs. Outage Duration

To achieve this plot, we calculated the grouped z-score by `CLIMATE.REGION` of all `OUTAGE.DURATION` and made the z-score threshold to be within approximately -0.5 to 0.5 to remove any significant outliers to give us a better representation to give us a more general comparison between all regions. 
<img width="1079" alt="image" src="climate_region_OD.jpg">

According to this plot, we observe the relationship between the different climate regions and different quartile measurements (1st quartile, Median, 3rd Quartile) of the outage durations of each regions with the East North Central Region having the highest median outage duration. 


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
Our Prediction Problem: We decided to use classification to do a binary classifer to predict the column 'CLIMATE.REGION' because we think it answers our central question: 'where are the causes of major outages?'

## Baseline Model

## Final Model

## Fairness Analysis
For the Fairness Analysis Model, we computed the difference in the distribution of the f1_score between the 'is_winter,' counting months [12, 1, 2] as 'is_winter' against the 'not_winter' group, in which we created a new is_winter column as a tranformation from the 'MONTH' column. We chose this analysis and thinks it supports our main argument 'where are the causes of major outages?' because while we we're making a new column for each 'Season' we realized that the outages in the month winter are disporportion to the other seasons. Therefore, we wanted to investigate if our model is fair based of the data.

Null Hypothesis: There are no differences between the distribution of the f1_scores of 'is_winter' and not 'is_winter'.
Alternate Hypothesis: There is a differences between the distribution of the f1_scores of 'is_winter' and not 'is_winter'.

<img width="1054" alt="image" src="https://github.com/user-attachments/assets/6b5d5b19-05d0-4d4a-99df-b3703f05d91b">
We utilized permutation test to test 'differences in f1_score distribution' between the 'is_winter' data and not 'not_winter' data. We got a p_value of: 0.13, which is greater than the observed statistic of 0.05, so we reject our null hypothesis and conclude that there is a differences between the distribution of the f1_scores of 'is_winter' and 'not_winter'.
