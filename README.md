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
ghgh

|     id |   average rating |   year published | is_healthy   | is_dessert   |   calories(#) |   sugar(PDV) |   saturated fat(PDV) |   protein(PDV) |   carbs(PDV) |
|-------:|-----------------:|-----------------:|:-------------|:-------------|--------------:|-------------:|---------------------:|---------------:|-------------:|
| 333281 |                4 |             2008 | False        | True         |         138.4 |           50 |                   19 |              3 |            6 |
| 453467 |                5 |             2011 | False        | False        |         595.1 |          211 |                   51 |             13 |           26 |
| 306168 |                5 |             2008 | False        | False        |         194.8 |            6 |                   36 |             22 |            3 |
| 286009 |                5 |             2008 | False        | True         |         878.3 |          326 |                  123 |             20 |           39 |
| 475785 |                5 |             2012 | False        | False        |         267   |           12 |                   48 |             29 |            2 |
---

## Assessment of Missingness

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