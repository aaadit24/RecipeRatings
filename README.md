# Recipe Rating Prediction: A Data Science Analysis

## Introduction
This analysis investigates recipe data from Food.com to understand and predict recipe ratings. The dataset contains 83,782 recipes with information about cooking time, ingredients, steps, and nutritional content. Our main question focuses on predicting recipe ratings based on recipe characteristics.

Relevant columns in our dataset:
- `minutes`: Time required to cook the recipe
- `n_steps`: Number of steps in the preparation
- `n_ingredients`: Number of ingredients used
- `nutritional values`: Including calories, fat, sugar, sodium, protein
- `avg_rating`: The target variable (scale of 1-5)


## Data Cleaning and Exploratory Data Analysis

### Cleaning Process
Initial examination revealed several data quality issues that required attention:
1. Cooking time outliers (some recipes listed as taking over 1 million minutes)
2. Missing ratings (2,246 missing values in avg_rating)
3. Complex nutritional information stored as strings

Our cleaning process included:
- Removing outliers in cooking time using the IQR method
- Dropping recipes with missing average ratings
- Converting nutritional information into separate numeric columns

[INSERT: Show cleaned DataFrame head]

### Univariate Analysis
The distribution of cooking times revealed important patterns:
- Most recipes require between 15-45 minutes
- Median cooking time is 30 minutes
- Distribution is right-skewed, with some recipes taking several hours

[INSERT: Add histogram of cooking times]

### Bivariate Analysis
When examining the relationship between cooking time and ratings:
- No clear correlation between cooking duration and rating
- Similar rating distributions across different cooking times
- High ratings (4-5 stars) dominate across all time ranges

[INSERT: Add scatter plot of cooking time vs ratings]

### Interesting Aggregates
Analyzing ratings across different recipe characteristics:
- Average ratings by cooking duration quartiles
- Rating distributions for different complexity levels
[INSERT: Add pivot table showing rating statistics by cooking duration]

## Assessment of Missingness

Our analysis of missing values revealed:
1. NMAR Analysis:
   - Rating column could be NMAR as users might be less likely to rate recipes they didn't make
   - Additional data about user behavior would be needed to confirm this

2. Missingness Dependency:
   - Found dependency: Rating missingness depends on number of steps (p-value = 0.0000)
   - Found no dependency: Rating missingness does not depend on cooking time (p-value = 0.8440)

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

## Final Model
Our final model built upon the baseline with additional engineered features:
1. steps_per_ingredient: Measures recipe complexity
2. time_per_step: Indicates instruction detail level

Model Improvements:
- Used GradientBoosting Regressor
- Implemented hyperparameter tuning
- All preprocessing in single sklearn Pipeline

Best Parameters:
- learning_rate: 0.01
- max_depth: 3
- n_estimators: 100

Performance:
- RMSE: 0.6224
- R² Score: 0.0001
- Improvement: 0.02%

## Fairness Analysis
Question: Does our model perform equally well for simple versus complex recipes?

Groups:
- Complex recipes (based on effort level)
- Simple recipes (based on effort level)

Results:
- RMSE for complex recipes: 0.6668
- RMSE for simple recipes: 0.6027
- Observed difference: 0.0640
- P-value: 0.0010

These results indicate that our model performs significantly differently between simple and complex recipes, raising fairness concerns that should be addressed in future iterations.

[INSERT: Permutation test visualization for fairness analysis]