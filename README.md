# Recipe Rating Prediction: A Data Science Analysis

## Introduction
This analysis investigates recipe data from Food.com to understand and predict recipe ratings. The dataset contains 83,782 recipes with information about cooking time, ingredients, steps, and nutritional content. Our main question focuses on predicting recipe ratings based on recipe characteristics.

[Table showing relevant columns and descriptions]
- Minutes: Minutes to prepare recipe
- N_steps: Number of steps in recipe
- N_ingredients: Number of ingredients
- [Add other relevant columns]

## Data Cleaning and Exploratory Data Analysis

### Cleaning Process
The primary cleaning steps included:
- Handling cooking time outliers using IQR method
- Removing missing values in average ratings
- Processing nutritional information

[INSERT: Show cleaned DataFrame head]

### Univariate Analysis
Distribution of cooking times shows most recipes take between 15-45 minutes, with a median of 30 minutes.

[INSERT: Add histogram of cooking times]

### Bivariate Analysis
Our analysis revealed no strong correlation between cooking time and recipe ratings.

[INSERT: Add scatter plot of cooking time vs ratings]

### Interesting Aggregates
[INSERT: Add pivot table showing rating statistics by cooking duration]

## Assessment of Missingness

The missingness analysis revealed:
- Rating missingness is dependent on number of steps (p-value = 0.0000)
- Rating missingness is independent of cooking time (p-value = 0.8440)

[INSERT: Add missingness test visualization]

## Hypothesis Testing
We tested whether cooking time influences recipe ratings.

Null Hypothesis (H0): No significant difference in average ratings between long and short cooking time recipes.
Alternative Hypothesis (H1): There is a significant difference in ratings between these groups.

Results:
- Observed difference: 0.0012
- P-value: 0.8060

[INSERT: Add hypothesis test visualization]

## Framing a Prediction Problem
**Prediction Task:** Predict the average rating of a recipe

**Type:** Regression problem (predicting a continuous value between 1-5)

**Response Variable:** avg_rating
- Represents the mean rating given to each recipe
- Scale: 1 to 5 stars

**Evaluation Metric:** Root Mean Square Error (RMSE)
- Chosen because:
  1. Same units as our predictions (stars)
  2. Penalizes larger errors more heavily
  3. Commonly used in rating prediction tasks

**Features Used for Prediction:**
- Recipe complexity indicators (minutes, n_steps)
- Recipe characteristics (n_ingredients)
- Nutritional information
- [Add other features used]

## Baseline Model
Our baseline model uses two key features:
1. minutes (numerical): Cooking time
2. calorie_quartile (categorical): Quartile categorization of calories

**Feature Processing:**
- Numerical features: Standardized using StandardScaler
- Categorical features: Encoded using OneHotEncoder

**Model Pipeline:**
1. ColumnTransformer for preprocessing both feature types
2. Linear Regression as the predictor
3. All steps implemented in a single sklearn Pipeline

**Performance:**
- RMSE: [Insert RMSE value]
- This score represents our baseline for improvement

[INSERT: Add visualization of baseline model predictions vs actual]