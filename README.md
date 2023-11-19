# Recipes and Rating Research Project

This is project 3 from DSC 80 course

By Javier Ponce


## Introduction

In recent years, the culinary landscape has witnessed a surge in interest and demand for vegan options due to the increase in popularity of veganism. Additionally, and in more recent years, there's been an active discussion about the impact of animal source foods on the environment and how to diminish it. As a reflection of this, we've seen the popularization of plant-based replacements for meats and other animal-source foods such as the IMPOSSIBLE burger. Personally, I am not vegan, in fact, I really like beef, but I do understand that diminishing our current consumption of meats and other animal sources of food is essential for the preservation of planet Earth. That is why, in this project, I am going to use a data set from Food.com to analyze veganism in the given data set, and at the end of this project, I'll answer if the data frame shows that we like Vegan foods or not.

As I've mentioned, the data I'll use in this project comes from Food.com. The data came from two different CSVs which I'll be using both as individual data frames and as a big merged one. The first CSV contains information about published recipies including their name, a unique recipe ID, minutes to prepare, contributor ID, date of the submission, tags, nutrition,steps, description, and ingridients. This csv is composed of 83782 different recipes. Then the secon CSV has infromation of different interactions that took place in Food.com. This interactions are describe by the following columns in the CSV, ID of the user who started the interaction, ID of the recipe, date of the interaction, a rating of stars, and a review if provided. This data frame has 731927 interactions.

As I've mentioned in this Project I aim to understand some of the Key characteristics that the data frames reflect about veganism. I want to understand how does the popularity of Veganism changed over time, and overall wheter or not we like vegan food the same as regular foods. To acomplish my goal of understanding veganismn more I'll start by Cleaning and doing a Exploratory Data Analysis over the most relevant columns to my question. Then I' asses the different type of missingness mechanisms that my data has and after that I'll do a Hypothesis test to answer wheter we like Vegan recipes more than normal recipes.

Since my focus on this project isto determine how much do we like vegan recipes relative to normal  recipes the essential columns fro my project would be rating (helping me asses if we like or not a recipe), both the date of interaction and the date of recipe submission (helping me see any kinds of trends over time), and an additional column that should help me determine if a recipe is vegan or not.

## Cleaning and EDA

### Data Cleaning	

The first thing I did to start my clening proces was to check the tyoes of the two data frames I had and look for a more convienient Type for each column.

**types for the recipes columns**
```
name              object
id                 int64
minutes            int64
contributor_id     int64
submitted         object
tags              object
nutrition         object
n_steps            int64
steps             object
description       object
ingredients       object
n_ingredients      int64
```

**types for the interaction columns**
```
user_id       int64
recipe_id     int64
date         object
rating        int64
review       object
```

#### Converting dates to date time tyoe.
The first thing I noticed and cleaned was the date columns, I noticed this columns where in the type of Object which is the type dessignated to strings in pandas. I changed this type to date time because date time is more convinient to do operations and to get informations from it.

#### Strings to lists.
Additionally, there are multiple columns in the recipes data frame which have data type of string but this are lists in the format of strings. Therefore i wrote a function that helped me tranfomed from a string to a list and I applied this function to the nescessary columns.

#### Nutrition column.
The nutrition column was one of the previous columns that had a string of a lists, but once I tranformed the strings into lists, I noticed that it was more convinient to transforme this list into different columns for each element.

#### Merged Data frame.
My last cleaning step was to form a new dataframe the merged the interactions and the recipes dataframes, for this I did an inner merging process, because it didn't make sense to keep values of either column if they didn't had a recipe from recipe or a interaction related to that recipe.

#### Look of the Data Frame


| user_id | recipe_id |	date | rating | Year_x | submitted | tags | calories |
|---------|-----------|------|--------|--------|-----------|------|----------|
| 483827 | 306785 | 2008-07-15 | 5 | 2008 | 2008-06-02 | [60-minutes-or-less, time-to-make,course, mai...| 95.3 |


