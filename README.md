# Introduction
### The datasets I chose is the "Recipes and Ratings". This project is going to explore the relationship between rating and time consumed and steps required on the recipes. People who are enjoying cooking, might want to know this question. How might time consumed and steps required affect the average rating on a recipe.
### There are two datasets in total, after merging them, there are 234429 rows in total. The col this project going to work on most are these four


| Column          | Description                     |
| :-------------- | ------------------------------: |
| `'minutes'`     | Minutes to prepare recipe       |
| `'n_steps'`     | Number of steps in recipe       |
|`'n_ingredients'`| Number of ingredients in recipe |
| `'submitted'`   | Date recipe was submitted       | 

---

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
  src="assets/histogram_of_cooking_n_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### As we can see, this plot shows mainly recipes are around 8 steps, it becomse rare when steps increase to 40. This could be helpful in later cutting off outliers.

## Bivariate Analysis

<iframe
  src="assets/n_steps_rating_scatter"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### As we can see, this scatter plot shows some relationship between n_steps and average rating: when the n_steps get larger, the rating tend to be higher.


## Interesting Aggregates

|   minutes |   0 |       1 |       2 |       3 |       4 |       5 |       6 |       7 |       8 |         9 |
|   n_steps |     |         |         |         |         |         |         |         |         |           |
|----------:|----:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|----------:|
|         1 |   5 | 4.79693 | 4.76968 | 4.696   | 4.75    | 4.72509 | 4.64865 | 4.50857 | 4.84615 | nan       |
|         2 | nan | 4.86538 | 4.76496 | 4.76011 | 4.70794 | 4.76921 | 4.80283 | 4.78571 | 4.7907  |   4.2     |
|         3 | nan | 4.708   | 4.75072 | 4.75973 | 4.6554  | 4.72072 | 4.76782 | 4.77493 | 4.75433 |   4.7619  |
|         4 | nan | 4.72705 | 4.75618 | 4.71963 | 4.67623 | 4.75903 | 4.67775 | 4.7234  | 4.73745 |   4.64286 |
|         5 | nan | 4.82073 | 4.74483 | 4.78999 | 4.64672 | 4.72717 | 4.62531 | 4.54998 | 4.51716 |   4.81132 |
|         6 | nan | 4.85714 | 4.79221 | 4.58807 | 4.51556 | 4.71538 | 4.62284 | 4.69601 | 4.74393 |   4.9     |
|         7 | nan | 5       | 4.92537 | 4.75    | 4.2962  | 4.60299 | 4.73882 | 4.75989 | 4.69458 |   4.68056 |
|         8 | nan | 4.78947 | 4.95238 | 4.64    | 4.67102 | 4.72086 | 4.78723 | 4.77941 | 4.63636 |   4.86036 |
|         9 | nan | 5       | 4.78947 | 4.57143 | 4.42308 | 4.81332 | 4.51938 | 4.80592 | 4.78125 |   4.625   |
|        10 | nan | 4.37778 | 4.83333 | 4.625   | 1.72727 | 4.70374 | 4.22597 | 4.38889 | 4.52381 |   4.66957 |

### Here is the pivot_table of `minuts` and `n_steps` with first 10 rows and 10 columns showing. It is somehow can see the rating decrese along the increase of n_steps, and rating increse along the increase of minutes

# Assessment of Missingness
## NMAR Analysis
### NMAR on user_id column
#### Even though missingness on user_id have relationship with the missingness on recipe_id and data.It does not depend on the value on recipe_id and date but the missingness. Bascially, The missingness present on these three at the same time is due to no review on the recipe.

### Solution_on_this_missingness
#### Since the reason behind is no one review the recipe, which imply the unpopular of this recipe, generally speaking, it suggests the lower averge rating on these recipe. Therefore, filling these missing value with a low rating among all possible recorded ratings is reasonable.

## Missingness Dependency
### In anayzing missingness on rating_filled column, n_steps column is chosen for checking missingness dependency. 
### Although the distribution of n_steps when rating_filled is missing and the distribution of n_steps when rating_filled is not missing looks similar. The permutation test revealed they are dependent.

<iframe
  src="assets/permutation_tvds_on_n_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### p_value is 0.0. 
#### Therefore, missingness on col rating_filled has missingness dependency with col n_steps

---

# Hypothesis Testing
### Null_Hypothesis = "n_steps and minutes will not affect rating."
### Alter_Hypothesis = "larger n_steps and minutes, result in higher rating."
#### Test Statistic: R^2
#### Reason for test statistic: regression line is closed to 0, and residual pattern looks random. Correlation factor should be near 0, looking for positive correlation to reject null.

#### Significant Level: 95%
#### Reason for 95% significant level: 95% significant level means the observed statistic is not located within 2 std around the mean, which gives a strong confidence to reject the null hypothesis.

## Firstly, the code using the whole dataset to run the permutation test, and failed

<iframe
  src="assets/fail_reject_null.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### It obtains a p_value around 0.297, which is way greater than 0.05, resulting fail to reject the Null_Hypothesis

### Then, try to alter the original question a little bit to `explore the relationship between rating and time consume and steps required on the recipes that take upto eight days`, since recipes that are over 8 days are more likely to be a joke, like "how to preserve a husband", which would result in a bad model training.
## Therefore, I restrict the recipe takes time only within 8 days.

<iframe
  src="assets/success_reject_null.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### It obtains a p_value of 0, which is good and reject the Null_Hypothesis.

---

# Framing a Prediction Problem
### The prediction problem chosen is `Given the cooking time(8 days maximum) and number of cooking steps, what would the rating of this recipe?`
#### Response variable is rating of the recipe. Rating means popularity of this recipe, for people who enjoys cooking, this could be an important parameter for them to try a certain recipe.
#### Since cooking time and number of cooking steps are all numerical values, the type of prediction is a Regression.
#### The evalutaion statistic chosen are R^2 and RMSE

---

# Baseline Model
### In the baseline model, following the prediction problem, literally it takes two features and then fit into a Linear Regression model:

| Column          | Description                     | Type          |
| :-------------- | ------------------------------: | ------------: | 
| `'minutes'`     | Minutes to prepare recipe       | quantitative  |
| `'n_steps'`     | Number of steps in recipe       | quantitative  |

### The performance of the model might not quite ideal.
### R^2 for training data is 0.00017, RMSE for training data is 0.499.
### R^2 for testing data is 0.00005, RMSE for testing data is 0.497.
### And I think current model is not good due to the underfitting model, this model is too basic, and my next steps is make it more complicated.
---

# Final Model
## The two extract features added are `'n_ingredients'` and `'submitted'`

| Column          | Description                     |
| :-------------- | ------------------------------: |
|`'n_ingredients'`| Number of ingredients in recipe |
| `'submitted'`   | Date recipe was submitted       | 

#### Adding feature `n_ingredients` is because the n_ingredients is somehow relate to n_steps. Literally, more ingredience involve would probabily result in longer cooking time and more cooking steps. So, the presence of n_ingredients could help to adjust misbehave of columns minutes and n_steps

#### Adding feature `submitted` is because the submitted is somehow relate to n_steps. Along with the time passing, the average of n_steps tend to be bigger. It makes sense that, the development of recipe, generating the variability of dishes making

<iframe
  src="assets/submitted_n_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### This scatter graph somehow support the reason added feature submitted, it shows the trend of time passing, the n_steps tend to get larger.

## In this part, two model algorithms are selected, SGDRegressor and LinearRegression.
### Performing GridSearchCV to search for the best combination of hyperparameter 'alpha' and 'loss' for SGDRegressor
#### where 'alpha' gives a just right regularization of training process, 'loss' provides the suitable solution to the outlier datapoints.

## In the Final_Model, comparing to the baseline_model:
### R^2 increases 0.014, RMSE decrease 0.0047 on train dataset;
### R^2 increases 0.009, RMSE decrease 0.0047 on test dataset.

## Overall, the final_model did have improvement over baseline_model.

---

# Fairness Analysis
## Null_Hypothesis:
### My model is fair. Its RMSE for recipes before 2009(inclusive) and recipes after 2009(exclusive) are roughly the same , and any differences are due to random chance."
## Alter_Hypothesis:
### My model is unfair. Its RMSE for recipes before 2009(inclusive) is less than recipes after 2009(exclusive), which means before2009_RMSE < after2009_RMSE ==> before2009_RMSE after2009_RMSE < 0

### Group_X is recipes before 2009(inclusive), Group_Y is recipes after 2009(exclusive)
### Since the Alter_Hypothesis is one-ended, Test statistic chosen is RMSE difference between before2009 and after2009

<iframe
  src="assets/differences_beforeAfter.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Conclusion: 
### Since the Alter_Hypothesis is looking for before2009_RMSE after2009_RMSE < 0, Then we should count more negative values as our p_value. Therefore, the p_value =  1.0 , which shows we fail to reject the Null_Hypothesis. As a result, the model might be fair respect to the different submitted time.
---
