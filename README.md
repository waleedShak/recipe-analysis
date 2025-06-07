# Analysis of Recipe Health
Author: Waleed Alshakhshir

---

## Introduction
In the advent of our fast-paced modern society and heavily processed food, the average person's diet has deteriorated significantly, leading to a plethora of diseases and health issues. Subsequently, it has become more important than ever for people to be conscious of what they eat and whether or not it’s healthy. This leads to an important question: **Is recipe health consciousness changing over time?** To answer this question, I will use two datasets collected from https://www.food.com/: `recipes` which contains unique recipes and `interactions` which contains user reviews of recipes.

`recipes` contains 83,782 rows and 12 columns where each row corresponds to a unique recipe.

| Column             | Description |
| :----------------- | :--------------------------------|
| `'name'`           | Name of the recipe|
| `'id'`             | Recipe ID |
| `'minutes'`        | Cooking time in minutes|
| `'contributor_id'` | ID of Recipe poster|
| `'submitted'`      | Date posted|
| `'tags'`           | Recipe tags|
| `'nutrition'`      | Recipe Nutrition information|
| `'n_steps'`        | Number of recipe steps|
| `'steps'`          | Recipe steps in order|
| `'description'`    | Recipe description |
| `'ingredients'`    | Recipe Ingredients |
| `'n_ingredients'`  | Ingredient number |

`interactions` contains 731,927 rows and 5 columns where each row corresponds to a user review of a recipe.

| Column        | Description         |
| :------------ | :------------------ |
| `'user_id'`   | Reviewer ID  |
| `'recipe_id'` | Recipe ID    |
| `'date'`      | Date of Review  |
| `'rating'`    | Rating given |
| `'review'`    | Text of Review |

---

## Data Cleaning and Exploratory Data Analysis

### Procedure
Before using and analysing the dataset to answer questions, we must first clean and prepare the data. The following section details the steps taken to prepare the data for analysis.

1. Merge Datasets:
	- Left merge `recipes` and `interactions` datasets on `'id'` and `'recipe_id'` to create a new dataset `study` which matches every recipe and its reviews.

1. Clean Ratings Column:
	- Replace 0 values in the `'rating'` column with NaN. This is done because ratings are on the scale 1 to 5 stars, so a 0 star rating actually indicates an unrated recipe.

1. Add column `'average rating'`:
	- A recipe can have multiple ratings from different reviews, so `'average rating'` is just the mean rating for a specific recipe.

1. Add column `'year published'`:
	- Extracts the year the recipe was posted from `'submitted'` 

1. Add column `'is_healthy'`:
	- Adds a boolean column `'is_healthy'` indicating whether healthy is one of the tags in the `'tags'` column.

1. Add column `'is_dessert'`:
	- Adds a boolean column `'is_dessert'` indicating whether dessert is one of the tags in the `'tags'` column.

1. Extract Nutrition Information from `'nutrition'`:
	- Uses `'nutrition'` to create the following columns: `'calories(#)'`, `'sugar(PDV)'`, `'protein(PDV)'`, `'saturated fat(PDV)'`, and `'carbs(PDV)'` where PDV stands for Percent Daily Value.

#### Result
After data preperation, the clean dataset `study` has 234429 rows and 26 columns. Due to the large number of columns, the following table only shows the most relevant columns of the first 5 unique rows of the dataset.

|     id |   average rating |   year published | is_healthy   | is_dessert   |   calories(#) |   sugar(PDV) |   saturated fat(PDV) |   protein(PDV) |   carbs(PDV) |
|-------:|-----------------:|-----------------:|:-------------|:-------------|--------------:|-------------:|---------------------:|---------------:|-------------:|
| 333281 |                4 |             2008 | False        | True         |         138.4 |           50 |                   19 |              3 |            6 |
| 453467 |                5 |             2011 | False        | False        |         595.1 |          211 |                   51 |             13 |           26 |
| 306168 |                5 |             2008 | False        | False        |         194.8 |            6 |                   36 |             22 |            3 |
| 286009 |                5 |             2008 | False        | True         |         878.3 |          326 |                  123 |             20 |           39 |
| 475785 |                5 |             2012 | False        | False        |         267   |           12 |                   48 |             29 |            2 |

### Univariate Analysis
#### Outliers
When trying to run univariate analysis, I ran into various outliers that would greatly distort visualizations and hinder understanding. To tackle this I used the IQR method to identify and remove outlier data.

#### Figures
This figure shows the distribution of sugar(PDV) in the dataset. The distribution is skewed to the right indicating that fewer recipes have a high amount of sugar. Futhermore, there exists a mode at the value: 0 showing that many recipes in the dataset don't use sugar all together. 
<iframe
  src="assets/uni_sugar.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

The plot shows the number of recipes published in each year of the dataset. The plot is right skewed with the latter years of the dataset having few entries. This could point to the site losing popularity since there are far fewer posts year on year.
<iframe
  src="assets/univariate_time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This figure analyzes the proportion of healthy recipes over time. As can be seen, the proportion of healthy recipes over time has a declining trend with 2018 recording the lowest healthy proportion across the years of this dataset.
<iframe
  src="assets/bivariate_time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates
| is_healthy   |   ('calories(#)', 'mean') |   ('calories(#)', 'median') |   ('calories(#)', 'std') |   ('calories(#)', 'max') |   ('sugar(PDV)', 'mean') |   ('sugar(PDV)', 'median') |   ('sugar(PDV)', 'std') |   ('sugar(PDV)', 'max') |   ('saturated fat(PDV)', 'mean') |   ('saturated fat(PDV)', 'median') |   ('saturated fat(PDV)', 'std') |   ('saturated fat(PDV)', 'max') |   ('protein(PDV)', 'mean') |   ('protein(PDV)', 'median') |   ('protein(PDV)', 'std') |   ('protein(PDV)', 'max') |   ('carbs(PDV)', 'mean') |   ('carbs(PDV)', 'median') |   ('carbs(PDV)', 'std') |   ('carbs(PDV)', 'max') |
|:-------------|--------------------------:|----------------------------:|-------------------------:|-------------------------:|-------------------------:|---------------------------:|------------------------:|------------------------:|---------------------------------:|-----------------------------------:|--------------------------------:|--------------------------------:|---------------------------:|-----------------------------:|--------------------------:|--------------------------:|-------------------------:|---------------------------:|------------------------:|------------------------:|
| False        |                   280.854 |                       255.8 |                  171.422 |                    989   |                  28.0718 |                         17 |                 29.1721 |                     126 |                         26.4913  |                                 20 |                        23.1342  |                              93 |                    25.6783 |                           16 |                   24.952  |                       101 |                  7.38257 |                          6 |                 5.85004 |                      25 |
| True         |                   221.754 |                       198.4 |                  134.652 |                    940.6 |                  33.6268 |                         23 |                 30.8937 |                     126 |                          8.75748 |                                  6 |                         9.90589 |                              80 |                    19.7474 |                           11 |                   21.4049 |                       101 |                  9.54034 |                          9 |                 6.11057 |                      25 |
---

## Assessment of Missingness
Of the columns present in the original merged dataset, 3 columns: 'description', 'rating', and 'review' have significant missing values. This section aims to analyse that missingness.

### NMAR Analysis
The missingness of the `'review'` column is most likely NMAR. Unless an average person thinks that a recipe is really good, really poor or in some other way intriging, they won't bother leaving a review. This is because writing a review for a recipe takes some time and effort that a mundane recipe isn't percieved to be worth.

### Missingness Dependency

---

## Hypothesis Testing

---

## Framing a Prediction Problem

---

## Baseline Model

---

## Final Model

---

## Fairness Analysis

---