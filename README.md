# My Project Title

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
1) tags: the tags associated with each recipe, initially stored as a string
2) rating: the rating assigned to each recipe, taken as the average rating from the accompanying 'interactions' dataset (float)
3) minutes: the number of minutes of preparation time listed for each recipe (int)

Additional Columns:
1) thirty-min-tag: indicates whether each recipe has the '30-minutes-or-less' tag (bool)
2) thirty-min-listed: indicates whether each recipe has a listed preparation time of <= 30 minutes

---

## Cleaning and EDA

The main steps that were taken to clean the dataset are as follows:
1) Merged the recipe dataset with the accompanying interactions dataset in order to add rating information to the recipes dataset.
 * Given that the rating system is on a scale of 1-5, ratings of 0 were not counted, since they likely represent missing ratings
2) Reformatted the 'tags' column to a list instead of a string in order to more easily access relevant tags.
3) Added additional columns that indicate whether a given recipe is listed with a sub-30-minute preparation time and/or has the '30-minutes-or-less' tag in order to facilitate analysis.

* Although there are other columns that could have been cleaned, such as the nutrition column, they were left alone since they were irrelevant to the analysis.

### Univariate Analysis
<iframe src="ua_fig1.html" width=800 height=600 frameBorder=0></iframe>

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
