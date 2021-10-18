# **EDA and Modelling of COVID-19 in Indonesia from January 2020 to July 2021**
the goal is to see how the actual development of COVID-19 in Indonesia at that period and visualize it.
## ABOUT
This study intends to investigate the present state of COVID-19 cases in Indonesia, where the number of cases impacted, recoveries, and deaths are all fluctuating between January 2020 and July 2021.
## Context
The COVID-19 dataset in Indonesia was created to find out various factors that could be taken into consideration in decision making related to the level of stringency in each province in Indonesia.
## Content
Data compiled based on time series, both on a country level (Indonesia), and on a province level. If needed in certain provinces, it might also be provided at the city / regency level. 


Demographic data is also available, as well as calculations between demographic data and COVID-19 pandemic data.
## Acknowledgements
The data is from https://www.kaggle.com/hendratno/covid19-indonesia, also Thank you to those who have provided data openly so that we can compile it into a dataset here, which is as follows: covid19.go.id, kemendagri.go.id, bps.go.id, and bnpb-inacovid19.hub.arcgis.com
## Data Description
Date | Reporting date.
Location ISO Code | Location codes based on ISO standards.

Location | Location name.

New Cases | New daily positive cases.

New Deaths | New daily deaths.

New Recovered | New daily recovered.

New Active Cases | New daily active cases.

Total Cases | Total positive cases until the related date.

Total Deaths | Total deaths until the related date.

Total Recovered | Total recovered until the related date.
## Data Preparation
• Code Used : RStudio

• Packages : "missForest", "Hmisc", "VIM", "VGAM", "tidyverse", "reshape2", 'ggstatsplot', "cleandata", "caret", "forecast", "caTools", "car", "psych", "car", "glmnet", "ggplot2", "dplyr", "tidyr", "patchwork"
## Total COVID-19 Cases in Indonesia per Location
How many total cases of Covid-19 there have been in Indonesia until now (9 July 2021).
![000058](https://user-images.githubusercontent.com/12520642/137746251-e4e0d50b-2509-436f-9992-c61400fb279b.png)

It turns out Jakarta has the biggest total number of cases compared to any other location. Perhaps it's because Jakarta is close to the location of the first COVID-19 case, which is Depok. And Jakarta is the city with the highest mobilization in the JABODETABEK area.

![000009](https://user-images.githubusercontent.com/12520642/137747145-42ebe0fb-33d5-4d3b-9308-49d64c52fd2e.png)

It turns out that 'Jawa' has the most total cases per island in Indonesia. Also, 'Jawa' has the biggest total number of cases compared to any other island in Indonesia. Perhaps because the first case of Covid-19 in Indonesia started in 'Jawa'.

## Four Highest Cases in Indonesia
![000029](https://user-images.githubusercontent.com/12520642/137747670-fc898d20-445d-4552-b7e6-1f8a5c840af4.png)

Maroon = 'DKI Jakarta'
Green = 'Jawa Barat'
Dark Blue = 'Jawa Tengah'
Gold = 'Jawa Timur'

If we look at the graph of the four greatest locations in terms of total new Covid-19 cases in the Java area, we can see that they all had a "peak" time that was nearly identical, namely around the beginning of the year in the months of December and January, with the largest being in June-July. However, if we look at this data, we can see that the overall number of new cases in West Java is higher than in Jakarta in the beginning of the year, and that as we approach the Eid vacation, specifically in the April-May period, the total number of cases in West Java is the highest in Indonesia.

## PSBB vs PPKM vs PPKM Emergency vs No Policy at all
![00001b](https://user-images.githubusercontent.com/12520642/137748651-10a0461e-1812-48d2-be56-f2b8418223f8.png)

Marron = PPKM
Green = PSBB
Blue = No Policy
Gold = PPKM Emergency

When the Indonesian government made a policy to apply PPKM, which was implemented on January 3, 2021, it was seen that at the beginning of its implementation, PPKM managed to reduce cases due to the absence of the PSBB policy, which was over on December 7, 2020, but the success of PPKM did not work due to the many who chose to take an Eid holiday. Because of the resultant increase in new cases at the Eid Holiday, the government implemented emergency PPKM (but in this dataframe it is not yet seen whether emergency PPKM has succeeded in reducing Covid-19 cases).

## PPKM Early Implementation
![000045](https://user-images.githubusercontent.com/12520642/137748932-9aafe54c-7432-4064-82c6-9f041be0aeb6.png)

It can be seen from the graph above that in the first week of implementing PPKM in Indonesia, there was an increase in cases, but after 5 days, the results were visible. It turned out that due to the implementation of PPKM, new cases began to decline, and the cure rate finally increased, and the mortality rate tends to be stable.
We can assume that the implementation of PSBB and PPKM in Indonesia has succeeded in reducing the number of cases, especially PPKM, and it seems that the Government of Indonesia should continue to implement a restrictive policy because it can effectively reduce the number of new cases in Indonesia (for emergency PPKM, it is still not concluded because there is no sufficient data to determine whether the emergency PPKM was successful).

## Split The Data for Modelling
Split Data : train – validation - test

## Feature Correlation
![00000b](https://user-images.githubusercontent.com/12520642/137749905-ab533557-e864-40e4-9c85-d352328dc2cf.png)

Collinearity problem happens when two independent variables are highly correlated with each other. From the output above, which is a pairplot, we can see that the variables many variables like : 

• New Cases - New Recovered 92% - New Death - drop New Recovered

• New Cases - Total Cases 83% - New Death - drop Total Cases

• New Cases - Total Death 82% - New Death - drop Total Death

• New Cases - Total Recovered 81% - New Death - drop Total Recovered

• New Cases - Total Active Cases 94% - New Death - drop Total Active Cases

is highly positively correlated with each other. Therefore, we will avoid using these 5 variables together in our regression model.

## Ridge and Lasso Regression
### Ridge Regression 
![1](https://user-images.githubusercontent.com/12520642/137751416-4d5528e6-9c1a-4483-a6f0-5b843eaf1597.PNG)

### Lasso Regression
![2](https://user-images.githubusercontent.com/12520642/137751670-532d41ce-13b1-4d0f-a04d-37331c8b10d7.PNG)

## Evaluating Model
![3](https://user-images.githubusercontent.com/12520642/137752565-4899fd8d-3b8a-4e01-a929-41499533bca2.PNG)

For MAE it means that On average, our prediction deviates the true admit_prob by 3.3 and also for RMSE The standard deviation of
prediction errors is 8.7 ○ i.e. from the regression line, the residuals mostly deviate between +- 8.7, unfortunately we can define the MAPE because of there is zero value in this data

![4 1](https://user-images.githubusercontent.com/12520642/137753536-bec71967-b45f-4b67-b8a3-9ce09f26c017.png)

For MAE it means that On average, our prediction deviates the true admit_prob by 3.3 and also for RMSE The standard deviation of prediction errors is 8.6 ○ i.e. from the regression line, the residuals mostly deviate between +- 8.6, unfortunately we can define the MAPE because of there is zero value in this data

Because There is zero value in the data that is why value of MAPE for both Ridge and Lasso respectively cannot be define.

## In Conclusion
This shows that the case of COVID-19 in Indonesia can be controlled if the government issues a policy regarding its handling. It also turns out that the PPKM actually helps. It has been proven from the start that the handling of PPKM has succeeded in reducing it. Based on this model prediction with Regularization Regression, the model that we use for prediction of New Deaths is: (2.262014e-02 New Cases) + (7.382256e-03 Active Cases) + (1.010345e-07 Population) + (-3.248394e-01 No Policy) + (2.416052e-01 PPKM) + (7.187393e+00 Emergency PPKM)


