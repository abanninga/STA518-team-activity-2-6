---
title: "Activity 2.6"
output: 
  html_document: 
    keep_md: yes
---



# Exploratory Data Analysis: Merging Data Sets and Visualizing Spatial Data

Requirements:

- GitHub account
- RStudio Cloud account

Goals:

- Join data sets

**Pick a lead**:
This person is not solely responsible for doing the activity, but they are responsible for organizing the collective team effort - for example, making sure all parts are completed and pushing them to the Team GitHub repo.

## Introduction

The late comedian [Mitch Hedberg](https://en.wikipedia.org/wiki/Mitch_Hedberg) believed that *La Quinta* is Spanish for "next to Denny's".

![Mitch HedLa Quinta](https://i.imgur.com/1S1YsA9.jpg)

In this activity, we will explore the validity of Mitch's joke by learning about merging data sets and visualizing spatial data.
This activity is based on a Mine Çetinkaya-Rundel lab.

## Getting started

We are still relying on only one Team Member (the lead) pushing the complete activity, but the others are expected to contribute to the discussion and help the lead member complete the step, but not *push* the files from their computer (they should be able to pull, though).

1. *All* Team Members:
  - Go to the Documents section on [Bb](https://mybb.gvsu.edu)
  - Click on the link titled `activity0206`
  - Click on the "Join" button next to your corresponding team name in the **Join an existing team** section
2. *All* Team Members now will:
  - In your team repo, click the green **Clone or download** button, select "Use HTTPS" if this isn't the default option, and click on the clipboard icon to copy the repo URL
  - Go to RStudio Cloud and into the course workspace.  Create a **New Project from Git Repo** - remember that you need to click on the down arrow next to the **New Project** button to see this option.
  - Paste the URL of your activity repo into the dialogue box.
  - Click "OK".
3. *All* Team Members now will Load Package:
  - In this lab, we will work with the `tidyverse` package so we need to install and load it.
    Type the following code into your *Console*:
  
    
    ```r
    install.packages("tidyverse")
    library(tidyverse)
    ```
    
  - Note that this package is also loaded in your R Markdown document.
4. *All* Team Members now will configure Git:
  - Go to the *Terminal* pane and type the following two lines of code, replacing the information inside the quotation marks with your GitHub account information:
  
    
    ```bash
    git config --global user.email "your email"
    git config --global user.name "your name"
    ```
    
  - Confirm that these changes have been implemented, run the following code:
  
    
    ```bash
    git config --global user.email
    git config --global user.name
    ```
        
  - Inform git that you want to store your GitHub credentials for $60 \times 60 \times 24 \times 7 = 604,800$ seconds, run the next line of code.  This needs to be done on a per-project basis.
  
    
    ```bash
    git config --global credential.helper 'cache --timeout 604800'
    ```
    
5. *All* Team Members will now name their RStudio project:
  - Currently your RStudio project is called *Untitled Project*.  Update the name of your project to be "Activity 2-6 - Merging"
6. The *Lead* Team Member to do the following in RStudio:
  - Open the `.Rmd` file and update the **YAML** by changing the author name to your **Team** name and date to today, then knit the document.
  - Go to the *Git* pane and click on **Diff** to confirm that you are happy with the changes.
  - *Stage* just your Rmd file, add a commit message like "Updated team name" in the *Commit Message* dialogue box and click **Commit**
  - Click on **Push**.  This will prompt a dialogue where you first need to enter your GitHub user name, and then your password - this should be the only time you need to do this for the current activity.
  - Verify that your changes have been made to your GitHub repo.
7. *All other* Team Members now will do the following in RStudio:
  - Go to the *Git* pane and click on **Pull** button.  This will prompt a dialogue where you first need to enter your GitHub user name, and then your password (this should be the only time you need to do this for the current activity).
  - Observe that the changes are now reflected in their project!

Again, only one team member will be pushing the changes.
All others are encouraged to work and save changes "locally" in RStudio.Cloud, but not push.

## The data

The data folder contains three csv files: one for Denny's locations, one for La Quinta's locations, and one for information on US states.


```r
dennys <- read_csv("data/dennys.csv")
laquinta <- read_csv("data/laquinta.csv")
states <- read_csv("data/states.csv")
```

The [Denny's](https://locations.dennys.com/) and [La Quinta](https://www.lq.com/en/findandbook/hotel-listings.html) locations were scrapped from the corresponding linked text.

For the US States data set, each observation represents a state, including DC.
Along with the name of the state, we have the two-letter abbreviation and geographic area of the state (in square miles).

***
**Exercise 1**:
What are the dimensions of the Denny's data set?
What does each row in the data set represent?
What are the variables?
Some inline functions that are helpful are `str`, `nrow`, `ncol`, `names`, `View`.

***

***
**Exercise 2**:
What are the dimensions of the La Quinta's data set?
What does each row in the data set represent?
What are the variables?
Some inline functions that are helpful are `str`, `nrow`, `ncol`, `names`, `View`.

***

We will limit our analysis to Denny's and La Quinta's locations within the United States.

***
**Exercise 3**:
Look at the websites that the data come from (linked above).
Are there any La Quinta's locations outside of the US?
If so, which countries?
What about Denny's?

***

***
**Exercise 4**:
Now take a look at the data.
What would be some ways of determining whether either establishment has any locations outside the US using just the data (and not the websites).
Don't worry about whether you know how to implement this yet, just brainstorm some ideas.
Include at least one as your answer, but you're welcomed to write down a few options too.

***

## Joining

We will determine whether the establishment has a location outside the US using the `state` variable in the `dennys` and `laquinta` data sets.
We know exactly which states are in the US, and we have this information in the `states` tibble we loaded.

***
**Exercise 5**:
Find the Denny's locations that are outside the US, if any.
To do so, *filter* the Denny's locations for observations where `state` is not in `states$abbreviation`.
The code for this is given below.
Note that the `%in%` operator matches the states listed in the `state` variable to those listed in `states$abbreviation`.
The `!` operator means **not**.
Are there any Denny's locations outside the US?

***

***
**Exercise 6**:
Add a `country` variable to the Denny's data set and set all observations to `"United States"`.
Remember that you can use the `mutate` function for adding a variable.
Make sure you save the result of this as `dennys` again so that the stored tibble contains the new variable for later exercises.

***

***
**Exercise 7**:
Find the La Quinta locations that are outside of the US and determine which country they are in.
This will probably require some Googling.
Take notes as you will need to use this information in the next exercise.

***

***
**Exercise 8**:
Add a `country` variable to the La Quinta data set.
Use the `case_when` function to populate this variable.
You will need to use your notes from Exercise 7 about which country the non-US locations are in.
Make sure you save the result of this as `laquinta`again so that the stored tibble contains the new variable for later exercises.
Some code to help get you started is provided:


```r
laquinta %>% 
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Columbia",
    ... # fill in the rest
  ))
```

***

For the rest of this activity, we will work with the data from the United States only.
All Denny's locations are in the US, so we do not need to worry about them.
However, you do need to filter the La Quinta data set for locations in the United States.
Add the following code after your solution to Exercise 8.


```r
laquinta <- laquinta %>% 
  filter(country == "United States")
```

***
**Exercise 9**:
Which states have the fewest Denny's locations?
What about La Quinta?
Is this surprising?
Why or why not?

***

Next we calculate which states have the most Denny's locations *per thousand square miles*.
This requires joining information from the Denny's data set with information from the `states` data frame.

First, count how many observations are in each state.
This will give you two variables: `state` and `n`.
Then, join this data frame with the `states` data frame.
Note that the variables in the `states` data frame that has the two letter abbreviations is called `abbreviation`.
Therefore, we need to specify that the `state` variable from the Denny's data should be matched `by` the `abbreviation` variable from the `states` date.


```r
dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

Look at the output from this code.
You will build on this pipeline in the next exercise.

***
**Exercise 10**:
Which states have the most Denny's locations per thousand square miles?
What about La Quinta?

***

Now we put the two data sets together (like we did in Activity 2.4).
However, before we do this, we need to add an identifier variable.
We will call this `establishment` and set the value to `"Denny's"` and `"La Quinta"` for the `dennys` and `laquinta` tibbles, respectively.
Add the following code after your solution to Exercise 9.


```r
dennys <- dennys %>% 
  mutate(establishment = "Denny's")
laquinta <- laquinta %>% 
  mutate(establishment = "La Quinta")
```

Since the two tibbles have the same columns (remember?), we can easily bind them with the `bind_rows` function.


```r
dennys_laquinta <- bind_rows(dennys, laquinta)
```

We can plot the locations of the two establishments using a scatter plot, and color the points by the establishment type.
Note that the latitude is plotted on the x-axis and the longitude is on the y-axis.


```r
ggplot(dennys_laquinta, mapping = aes(x = longitude, y = latitude, color = establishment)) +
  geom_point()
```


The following two questions ask you to create visualizations.
These should follow best practices such as informative titles, axis labels, etc.
See [http://ggplot2.tidyverse.org/reference/labs.html](http://ggplot2.tidyverse.org/reference/labs.html) for help with the syntax.
You can also choose different themes to change the overall look of your plots.
See [http://ggplot2.tidyverse.org/reference/ggtheme.html](http://ggplot2.tidyverse.org/reference/ggtheme.html) for help with these.

***
**Exercise 11**:
Filter the data for observations in Michigan only, and create a plot.
You should also adjust the transparency of the points, by setting the `alpha` level, so that it is easier to see the over-plotted ones.
Visually, does Mitch Hedberg's joke appear to hold here?
***

***
**Exercise 12**:
Now filter the data for observations in Texas only.
Create the plot, with an appropriate `alpha` level.
Visually, does Mitch Hedberg's joke appear to hold here?

***

Feeling creative? 
Exploring [`geom_polygon`](https://eriqande.github.io/rep-res-web/lectures/making-maps-with-R.html).

Have your **Lead Team Member** commit and push the final activity to your Team's repo.

