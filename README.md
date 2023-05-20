# To Tag or Not to Tag?

by Nicholas Jumaoas 

---

## Introduction

This will be an analysis of '30-minute' recipes from food.com. While all recipes from the dataset are accompanied
by a listed preparation time, not all recipes with a listed preparation time of 30 minutes or less are tagged with
the '30-minutes-or-less' tag. As such, this project will endeavor to determine whether there is a significant
difference in rating among tagged and untagged recipes with sub-30-minute listed preparation times.

### Dataset Information

Number of rows: 83781

Relevant Columns: 

1. tags: the tags associated with each recipe, initially stored as a string 

2. rating: the rating assigned to each recipe, taken as the average rating from the accompanying 'interactions' dataset (float)  

3. minutes: the number of minutes of preparation time listed for each recipe (int)  

Additional Columns:  

4. thirty_min_tag: indicates whether each recipe has the '30-minutes-or-less' tag (bool)  

5. thirty_min_listed: indicates whether each recipe has a listed preparation time of <= 30 minutes

---

## Cleaning and EDA

The main steps that were taken to clean the dataset are as follows:

1. Merged the recipe dataset with the accompanying interactions dataset in order to add rating information to the recipes dataset.  

   > Given that the rating system is on a scale of 1-5, ratings of 0 were not counted, since they likely represent missing ratings.

2. Reformatted the 'tags' column to a list instead of a string in order to more easily access relevant tags.

3. Added additional columns that indicate whether a given recipe is listed with a sub-30-minute preparation time and/or has the '30-minutes-or-less' tag in order to facilitate analysis.

   > Although there are other columns that could have been cleaned, such as the nutrition column, they were left alone since they were irrelevant to the analysis.
  

An excerpt of the relevant collumns of the cleaned dataset can be viewed here:  

| tags                                                                                                                                                                                                                                                                                               |   rating |   minutes | thirty_min_tag   | thirty_min_listed   |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------:|----------:|:-----------------|:--------------------|
| ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        4 |        40 | False            | False               |
| ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        5 |        45 | False            | False               |
| ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |        5 |        40 | False            | False               |
| ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |        5 |       120 | False            | False               |
| ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |        5 |        90 | False            | False               |       

### Univariate Analysis
<iframe src="ua_fig1.html" width=800 height=600 frameBorder=0></iframe>  

The most relevant column to analyze is, of course, that of the ratings of the recipes, since that is the primary metric by which the recipes will be judged.
A particularly eye-catching feature of this graph is the heavy bias towards higher ratings, which could indicate that users are more likely to leave reviews 
with ratings when they are especially satisfied with a recipe. Additionally, the spike at a four-star rating is probably due to a general tendency towards
'round' numbers, as opposed to more granular ratings.

### Bivariate Analysis
<iframe src="ba_fig1.html" width=800 height=600 frameBorder=0></iframe>  

Featuring a side-by-side comparison of ratings across the categorical variables of listed and tagged rows, it is immediately apparent that each distribution, 
including the baseline, contains a large amount of outliers. This is due to the heavy tendency of users to gravitate towards higher ratings, as alluded to in 
the univariate analysis. Notably, while the distribution of the 'listed' boxplot is almost identical to that of the larger dataset, the distribution of the 
'tagged' boxplot is noticeably weighted downwards, with a first quartile approximately .07 points lower than the other two distributions. This reflects the 
apparent tendency of tagged recipes to have worse performance, which was the driver behind this analysis.

### Interesting Aggregates

|                |   mean_rating |   count |
|:---------------|--------------:|--------:|
| (False, False) |       4.60959 |   46454 |
| (False, True)  |       4.85747 |      15 |
| (True, False)  |       4.67161 |   16696 |
| (True, True)   |       4.62278 |   20616 |

Displayed is a table of nested groups, wherein the first boolean indicates whether a recipe is listed with a <=30min preparation time and the second boolean 
indicating whether that recipe was also tagged with the '30-minutes-or-less' tag. Most notably, there are very few recipes that tagged as taking 30 minutes or less
despite having a listed preparation time of more than 30 minutes. Noticeably, however, among recipes that are listed as taking 30 minutes or less to prepare, there
is a sizeable gap in mean rating between tagged and untagged recipes, with untagged recipes being generally rated higher than their untagged counterparts. This 
could potentially indicate some sort of negative bias against tagged recipes.

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing


---
