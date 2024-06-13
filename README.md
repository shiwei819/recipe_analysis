# Introduction
### The datasets I chose is the "Recipes and Ratings". This project is going to explore the relationship between rating and time consumed and steps required on the recipes. People who are enjoying cooking, might want to know this question. How might time consumed and steps required affect the average rating on a recipe.
### There are two datasets in total, after merging them, there are 234429 rows in total. The col this project going to work on most are these four

| Column | Description |
|: ----------- | :----------- |
| 'minutes' | Minutes to prepare recipe |
| 'n_steps' | Number of steps in recipe |
| 'n_ingredients | Number of ingredients in recipe |
| 'submitted' | Date recipe was submitted | 

# Data Cleaning and Exploratory Data Analysis
## Data Cleaning
### First, as I need to access to all recipes existed in recipe dataset, I read and left merge recipe dataset and interaction dataset(containing rating) respect to the recipe_id. 
### Second, replace rating that equals to zero with np.NaN, because a rate of zero is due to no input of rating.
### Third, using mean of each recipe to fill the missing ratings in the same recipe

|    | name                                 |   minutes | submitted   |   n_steps |   n_ingredients |   rating |   rating_filled |
|---:|:-------------------------------------|----------:|:------------|----------:|----------------:|---------:|----------------:|
|  0 | 1 brownies in the world    best ever |        40 | 2008-10-27  |        10 |               9 |        4 |               4 |
|  1 | 1 in canada chocolate chip cookies   |        45 | 2011-04-11  |        12 |              11 |        5 |               5 |
|  2 | 412 broccoli casserole               |        40 | 2008-05-30  |         6 |               9 |        5 |               5 |
|  3 | 412 broccoli casserole               |        40 | 2008-05-30  |         6 |               9 |        5 |               5 |
|  4 | 412 broccoli casserole               |        40 | 2008-05-30  |         6 |               9 |        5 |               5 |

## Univariate Analysis
<iframe
  src="histogram_of_cooking_n_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Assessment of Missingness

# Hypothesis Testing

# Framing a Prediction Problem

# Baseline Model

# Final Model

# Fairness Analysis