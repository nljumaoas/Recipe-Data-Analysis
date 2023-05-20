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

Relevant Columns: <br>
1) tags: the tags associated with each recipe, initially stored as a string <br>
2) rating: the rating assigned to each recipe, taken as the average rating from the accompanying 'interactions' dataset (float) <br>
3) minutes: the number of minutes of preparation time listed for each recipe (int) <br>

Additional Columns: <br>
1) thirty-min-tag: indicates whether each recipe has the '30-minutes-or-less' tag (bool) <br>
2) thirty-min-listed: indicates whether each recipe has a listed preparation time of <= 30 minutes

---

## Cleaning and EDA

The main steps that were taken to clean the dataset are as follows: <br>
1) Merged the recipe dataset with the accompanying interactions dataset in order to add rating information to the recipes dataset. <br>
> Given that the rating system is on a scale of 1-5, ratings of 0 were not counted, since they likely represent missing ratings. <br>
2) Reformatted the 'tags' column to a list instead of a string in order to more easily access relevant tags. <br>
3) Added additional columns that indicate whether a given recipe is listed with a sub-30-minute preparation time and/or has the '30-minutes-or-less' tag in order to facilitate analysis. <br>

> Although there are other columns that could have been cleaned, such as the nutrition column, they were left alone since they were irrelevant to the analysis.  

An excerpt of the relevant collumns of the cleaned dataset can be viewed here:  

name	id	minutes	contributor_id	submitted	tags	nutrition	n_steps	steps	description	ingredients	n_ingredients	rating	thirty_min
1486	almond cookie bites	401761	16	1434673	2009-11-29	[30-minutes-or-less, time-to-make, course, mai...	[40.1, 3.0, 4.0, 1.0, 0.0, 8.0, 1.0]	16	['preheat oven to 350 degrees f', 'in medium b...	NaN	['all-purpose flour', "fisher chef's naturals ...	9	2.666667	True
3087	apricot gorgonzola crescent appetizers	332410	40	991676	2008-10-22	[60-minutes-or-less, time-to-make, course, mai...	[139.9, 11.0, 15.0, 7.0, 6.0, 13.0, 4.0]	17	['heat oven to 350f spray large cookie sheet w...	NaN	['pillsbury refrigerated crescent dinner rolls...	6	4.666667	False
3685	asparagus milanese	382664	15	714468	2009-07-24	[15-minutes-or-less, time-to-make, course, mai...	[225.2, 26.0, 13.0, 7.0, 23.0, 45.0, 3.0]	16	['snap off the tough ends of the asparagus', '...	NaN	['asparagus', 'parmigiano-reggiano cheese', 'b...	5	4.500000	False
5803	baked yams with spicy molasses butter	382792	75	714468	2009-07-25	[time-to-make, course, main-ingredient, prepar...	[482.9, 24.0, 27.0, 5.0, 8.0, 49.0, 27.0]	10	['using electric mixer , beat first 7 ingredie...	NaN	['unsalted butter', 'molasses', 'ground cinnam...	8	5.000000	False
5983	balthazar s brioche french toast	378728	25	714468	2009-06-24	[30-minutes-or-less, time-to-make, course, pre...	[836.3, 39.0, 84.0, 42.0, 63.0, 67.0, 40.0]	14	['in a large bowl , whisk together eggs , suga...	NaN	['eggs', 'superfine sugar', 'milk', 'ground ci...	10	3.000000	True
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
79329	ultimate screwdriver	423077	2	1596512	2010-05-04	[15-minutes-or-less, time-to-make, course, pre...	[40.6, 0.0, 30.0, 0.0, 1.0, 0.0, 3.0]	3	['fill glass with ice', 'add smirnoff orange f...	NaN	['smirnoff orange vodka', 'orange juice']	2	5.000000	False
80877	voodoo chicken with sweet and sour onions ro...	383510	30	714468	2009-07-31	[30-minutes-or-less, time-to-make, course, mai...	[263.4, 7.0, 33.0, 3.0, 53.0, 4.0, 3.0]	8	['preheat oven to 400f coat a rimmed baking sh...	NaN	['boneless skinless chicken breast', 'salt and...	8	5.000000	True
81188	wasatch mountain chili	290480	50	778477	2008-03-06	[60-minutes-or-less, time-to-make, course, pre...	[672.9, 42.0, 25.0, 54.0, 65.0, 33.0, 25.0]	4	['in a large saucepan over medium heat cook on...	NaN	['onion', 'olive oil', 'hominy', 'great northe...	14	5.000000	False
81701	white bean chicken chili giada de laurentiis	430591	75	714468	2010-06-22	[time-to-make, course, main-ingredient, prepar...	[409.0, 21.0, 8.0, 35.0, 87.0, 18.0, 10.0]	13	['in a large heavy-bottomed saucepan or dutch ...	NaN	['olive oil', 'onion', 'garlic cloves', 'groun...	18	5.000000	False
83070	yukon gold potatoes jacques pepin style	387006	20	714468	2009-08-25	[30-minutes-or-less, time-to-make, preparation...	[292.1, 11.0, 15.0, 9.0, 14.0, 20.0, 16.0]	7	['place the potatoes in a deep skillet and add...	NaN	['yukon gold potatoes', 'salt', 'fresh ground ...	6	4.000000	True
70 rows × 14 columns

name                0
id                  0
minutes             0
contributor_id      0
submitted           0
tags                0
nutrition           0
n_steps             0
steps               0
description        27
ingredients         0
n_ingredients       0
rating            518
thirty_min          0
dtype: int64
| tags                                                                                                                                                                                                                                                                                               |   rating |   minutes | thirty_min_tag   | thirty_min_listed   |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------:|----------:|:-----------------|:--------------------|
| ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        4 |        40 | False            | False               |
| ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        5 |        45 | False            | False               |
| ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |        5 |        40 | False            | False               |
| ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |        5 |       120 | False            | False               |
| ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']       

### Univariate Analysis
<iframe src="ua_fig1.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="ua_fig2.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="ua_fig3.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
<iframe src="ba_fig1.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates


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
