# Recipe Rating Analysis and Prediction

## Introduction
This analysis explores the relationship between recipe characteristics and their ratings from Food.com. Our investigation centers around understanding what factors influence recipe ratings and developing a model to predict recipe ratings based on various features. The dataset contains 73,545 recipes with 12 relevant columns including cooking time, number of steps, ingredients, and nutritional information.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning Process
Our initial data cleaning steps included:
1. Removing recipes with missing ratings
2. Handling cooking time outliers using the IQR method
3. Processing nutritional information into separate columns

[INSERT: Add a DataFrame.head() screenshot showing the cleaned data structure]

### Univariate Analysis
The distribution of cooking times shows most recipes take between 15-45 minutes to prepare, with a median of 30 minutes.

[INSERT: Add the histogram of cooking times distribution]

### Bivariate Analysis
When examining the relationship between cooking time and average ratings, we found no strong correlation between these variables.

[INSERT: Add the scatter plot of cooking time vs ratings]

### Interesting Aggregates
Looking at recipe ratings across different cooking duration categories:

[INSERT: Add the aggregated table showing rating statistics by cooking duration]

## Assessment of Missingness

In our dataset, we observed two columns with missing values:
- Rating: 6.11% missing
- Average Rating: 1.12% missing

The missingness dependency analysis revealed:
- Rating missingness depends on the number of steps (p-value = 0.0000)
- Rating missingness does not depend on cooking time (p-value = 0.8440)

[INSERT: Add the permutation test visualization for missingness]

## Hypothesis Testing

Research Question: Do recipes with longer cooking times tend to receive different ratings than recipes with shorter cooking times?

Null Hypothesis (H0): There is no significant difference in average ratings between recipes with long cooking times and recipes with short cooking times.

Alternative Hypothesis (H1): There is a significant difference in average ratings between recipes with long and short cooking times.

Results:
- Observed difference in means: 0.0012
- P-value: 0.8060

[INSERT: Add the permutation test visualization for hypothesis test]

Based on our analysis, we failed to reject the null hypothesis, suggesting that cooking time does not significantly influence recipe ratings.

[Continue with the remaining sections...]