# Data 102 Final Project: Modeling U.S. Asthma Prevalence and Particulate Matter 2.5 Concentrations

Overview: 
In this project, we analyzed datasets containing information about daily PM2.5 Concentrations throughout the United States and the prevalence of tobacco use and asthma to answer these two questions:

1. “Does the data for asthma prevalence and 24-hr Avg. PM2.5 concentrations differ at different stratification and scales?”
2. “Do higher levels of PM2.5 cause higher levels of asthma?” 

## Modeling, Inference, and Decisions
We used a combination of multiple hypothesis testing and causal inference techniques to answer our two main questions.

For multiple hypothesis testing, we had five hypotheses:
1. Is there a difference in U.S. states' asthma rates from 2011 to 2014?
2. Is there a difference in U.S. states' asthma rates across males and females?
3. Is there a difference in U.S. states' asthma rates across White, Non-Hispanic and Hispanic?
4. Is there a difference in county 24-hr average PM2.5 concentrations across LA and Alameda County?
5. Is there a difference in state 24-hr average PM2.5 concentrations across California and Texas?

We applied the correction procedures of Bonferroni and Benjamini-Hochberg, controlling for FWER
and FDR respectively. The same discoveries remain significant in both procedures. This is likely due to the fact that their p-values were 0, which strongly suggests that the original samples do not have the same underlying distribution.

We avoided p-hacking by writing our questions first and sticking to the same sampling and statistical procedures. For example, for the asthma prevalence, we take the absolute difference between the averaged asthma prevalence from both distributions; for the 24-hr Avg. PM2.5 concentrations, we take the absolute difference between the 50th percentile from both distributions. We chose average for asthma prevalence as the distributions appear approximately normal, but chose 50th percentile for 24-hr Avg. PM2.5 concentration due to the distributions having a significant right-skew caused by outliers—likely due to weather and environmental conditions such as wildfire season.

## Causal Inference
To adjust for the confounding variables, we considered the outcome regression technique since we were working with an unconfoundedness assumption and attempted to fit an OLS model to account for relevant covariates across our merged dataset. This was to help us check if the mean squared error and treatment coefficient would indicate a possible linear interaction between our treatment and outcome variables on a linear model, given the selected covariates. We also implemented the inverse propensity weighting and propensity scores from the treatment variable made based on the ds_pm_pred values to see if there is a significant treatment effect between high and low PM2.5 values conditioning on the covariates. We couldn’t use exact matching because the data values for the PM2.5 dataset were aggregated across each state per year in 2011-2014, which would impact the exact conditions of the relevant confounding factors we’re looking for in the asthma set.

To estimate causal inference, we found a variety of R-squared values, calculated the simple difference in the observed group means, accounted for counfoundedness, and created an OLS model including the treatment variable. We then ran the OLS model with no intercept and calculated the mean squared error. Lastly, we used a logistic regression model to perform inverse propensity weighting.

## More Detailed Information
The Final Project.ipynb notebook and Final Project Report contain all the code and information related to the project. The report gives a much more detailed overview about the methods used and process for filtering the data sets for EDA and model implementations, including the ovrall conclusion.

## Files
1. Daily_Census_Tract-Level_PM2.5_Concentrations__2011-2014.csv
  - Contains information on daily PM2.5 concentration levels within each geographic area within the US

2. smaller_PM2.5.csv
  - A smaller portion of the U.S. Chronic Disease Indicators dataset with about 200,000 rows (~50,000 for each year between 2011-14 evenly shuffled)
  - Contains information about tobacco and asthma prevalence within each state

## References 
“Particulate Matter (PM2.5) Trends.” EPA, Environmental Protection Agency, 26 May 2021, www.epa.gov/air-trends/particulate-matter-pm25-trends.
