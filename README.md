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

#### A look to the Data Frame


| user_id | recipe_id |	date | rating | Year_x | submitted | tags | calories |
|---------|-----------|------|--------|--------|-----------|------|----------|
| 483827 | 306785 | 2008-07-15 | 5 | 2008 | 2008-06-02 | [60-minutes-or-less, time-to-make,course, mai...| 95.3 |

This is how the first row of the most important columns look like

#### Finding how to determine if a recipe is vegan.
When I first though of my question I didn't know if there was going to be a way to tell appart vegan recipes from not vegan recipes. My initial though was that I could look through all the ingridients and classify  which ingrdients made a recipe not vegan and then classify each recipe with their respective ingrdients. I immediatly realized that this was not going to be possible since the number of ingridients is huge and to classify the ingridients I would have to do it manually. Instead then, I though about looking in the tags, and that maybe there was a vegan tag I could use to my advantage. Fortunately for my I found a tag named vegan and with this I was able to created a new column which had True if a recipe was vegan and False otherwise.

### Univariate Analysis	

Now, after doing all the mentioned modification to my Data frame we are able to do some Analysis.

First I wanted to understand the distribution of recipes and interactions over the years, To build a better understanding of the data set overall.

<iframe src="assets/recipesdist.html" width=800 height=600 frameBorder=0></iframe> 

<iframe src="assets/interactions_years.html" width=800 height=600 frameBorder=0></iframe>

In this histograms we see how both recipes and interactions decrease over time, which means that most of the data comes from the early yers of the website while very few data come from the last years. This could be a consequence of a decrease on the active users of the website over the years, since less users would make fewer publications and fewer interactions.

Then I was curious to see how did the distribution of ratings look, this would help us understand what a low rating would be compared to all the ratings in general.

<iframe src="assets/ratingsdist.html" width=800 height=600 frameBorder=0></iframe> 

Now with this histogram we can understand more what does each rating mean, for example getting a 3 star rating migh not seem so bad, after seeing this histogram you can see that 3 star ratings are part of the lowest 7 percent of ratings, which makes a 3 star rating a low value more than a mid range value.

### Bivariate Analysis	

Now it is time to do a more interesting analysis that compares vegan recipes with other variables of the data.

The first think I though about checking was how do the number of vegan recipies changes as years go by, but as we saw in the Univariate Analysis the number of recipies decreases over the years regardless of the recipes being vegan or not vegan. Therefore if I wnated to find a significant increase in the popularity of vegan recipes I needed to compare the proportion of vegan recipies each year.

<iframe src="assets/proportion_of_vegan_years.html" width=800 height=600 frameBorder=0></iframe> 

Here we see and initial increase in the proportion of vegan recipes each year. Which could support the argument that vegan recipes had an increase in popularity on that period of time. But then we se a rapid decrease in this proportions, this could be to the deacrese of active users on the website as I mentioned in my univarite analysis.

Since I want to understand if vegan recipes are rated different to normal recipes, the next thing I checked  was the distribution of ratings for Vegan recipes only.

<iframe src="assets/vegan_ratings.html" width=800 height=600 frameBorder=0></iframe> 

Here we see that the ratings of vegan recipes are very similar to the ratings of all recipes over all. Both distribution have a higher concentration in high ratings, but if we look carefully it seems as if the vegan recipes have more concentration on the high end of the ratings than the overall distribution of ratings.

### Interesting Aggregates	

In this section I want to show some interesting tables I formulated that bring information about the nutritional value of vegan recipes.

| vegan/rating | 0 | 1 | 2 | 3 | 4 | 5 |
|--------------|---|---|---|---|---|---|
| False | 49.703116 | 48.088483 | 44.777281 | 41.679254 | 38.057655 | 40.767469 |
| True | 10.479514 | 18.125926 | 10.780303 | 10.500000 | 8.912019 | 10.033976 |

**The table above represents the average saturated fats from vegan and non vegan recipes at each of the specified ratings**

| vegan/rating | 0 | 1 | 2 | 3 | 4 | 5 |
|--------------|---|---|---|---|---|---|
| False | 492.085406 | 495.705484 | 457.860599 | 435.136629 | 413.99717 | 423.388873 |
| True | 309.517602 | 302.031852 | 255.820455 | 251.997541 | 253.47250 | 260.301493 |

**The table above represents the average calories from vegan and non vegan recipes at each of the specified ratings**


Looking at this differnt tables you can understand a little bit more about how different is the nutrition of vegan recipes compared to regular recipes and how the nutriciuos facts reflect in the rating. The first thing I noticed in this tables, is that compared to non-vegan recipes, vegan recipes tend to have lower values in all categories on average than non-vegan recipes, this could be the reason why vegan foods are normally consider healthy since the excess of most of this nutrition categories is bad for your haelth,and having lower values on everything helps moderation. Additionaly, these tables help to see how rating chnages with the nutrition, we see in most of the tables that the lowest rating is assign to the highest values which means that normally users don't like food that have excess of calories, fats, sugar, etc. In addition, we see that in most of the tables the highest ranking comes with a mid range values showing that we don;t like the excess but also we don't particularly like when a food has very low calories, sugars,etc.

## Assessment of Missingness

### NMAR Analysis

After looking at my columns with missing values above, I believe that the missingness of description is NMAR, this is because this would be a person who writes a recipe and thinks that the description would be too simple and therefore they don't include one. For example if I am doing a ham and cheese sandwich my description would be too simple and obvious that I might not include it on the page. Therefore since the missing description depends on the description being simple this is NMAR.

### Missingness Dependency	

After looking at the missingness of 'reviews',  I realized that the year of the interactions(Year_x) are in the higher end of years, which is very odd since most of the data on both recipes and interactions came from the earlier years, then looking at the years of the recipes (Year_y) I noticed that this were on the earlier years just like expected, which makes me think that the missingness of review might be **MAR** dependent on the year of the review.

<iframe src="assets/missing_reviews1.html" width=800 height=600 frameBorder=0></iframe> 

Here we can clearly see how most of the missing reviews come from the last three years which as I said is very odd because we have more data from the early 2000's. So let's ran a simulation to see if this is MAR. Our null will be that the years of the missing reviews were selected randomly from the distribution. our alternative would be that this years where not seledcted at random and therefore the missing reviews depend on the Year_x column.

To check this i generated a data set of expected TVD's if the years were randomly selected from the years of the ratings availible.

<iframe src="assets/MARtest.html" width=800 height=600 frameBorder=0></iframe> 

Here we can see how far away is out observed TVD compared to the expected TVD'S from the simulation. This helps us reject the null suggesting that the missing reviews are dependednt on the year of the interaction **note the probabilities I used for our null where the proportions from the histogram of the distribution of interactions over the years**

Now if we look at the distribution of the missing reviews over the year of the submission we will see that this distribution is extremely similar to the distribution of recipes over the years, showing that it is not dependent on this column.

<iframe src="assets/missing_reviews2.html" width=800 height=600 frameBorder=0></iframe> 

## Hypothesis Testing
 After cleaning and analizing the data, I am goint to do a hypothesis test to answer the question, **Do vegan recipes get better ratings than regular recipes?**

 To answer my question my null Hypothesis is going to be

**Null hypothesis: Vegan recipes get the same ratings than non-vegan recipes**

and my alternative hypothesis will be

**Alternative hypothesis: Vegan recipes get better ratings than non-vegan recipes**

To solve this question my test statistic is going to be the average rating for vegan recipes minus the average rating of non-vegan recipes

After doing a simulation here you can see the observed test statistic compared to the simulated test statistics.

<iframe src="assets/hypothesis_test.html" width=800 height=600 frameBorder=0></iframe> 

Here we see that our observed test statistic is in the higher end of the yielding a p value of 0.007, which is enough to reject the null. As in all hypothesis testing this does not mean that we accept the alternative, we can never be sure of any of the hypothesis, but with this experiment we can conclude that the data does reflect a slighty better perfomance of vegan recipes in the Food.com website.






