# Analysis of Recipe Health
Author: Waleed Alshakhshir

---

## Introduction
In the advent of our fast-paced modern society and heavily processed food, the average person's diet has deteriorated significantly, leading to a plethora of diseases and health issues. Subsequently, it has become more important than ever for people to be conscious of what they eat and whether or not it’s healthy. This leads to an important question: **Are recipes becoming healthier over time?** To answer this question, I will use two datasets collected from https://www.food.com/: `recipes` which contains unique recipes and `interactions` which contains user reviews of recipes.

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

#### result
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


### Bivariate Analysis

### Interesting Aggregates
---

## Assessment of Missingness
### NMAR Analysis

### MAR Analysis
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