# Movies
![pexels-tima-miroshnichenko-7991579](https://github.com/ksadangrit/Movies/assets/156267785/48e0806f-548b-43d7-98df-ffd9d420c4ff)

_Photo by Tima Miroshnichenko from [Pexels](https://www.pexels.com/photo/cartoon-movie-showing-on-theater-screen-7991579/)_

## Introduction
This dataset is scrapped from IMDb by Daniel Grijalva and is available to download on [Kaggle](https://www.kaggle.com/datasets/danielgrijalvas/movies). The dataset contains information about movies from between 1986 - 2020.



Click here for the [license](https://creativecommons.org/publicdomain/zero/1.0/).

## Importing data
Download the csv file for the movie data from Kaggle
Importing data into a spreadsheet by selecting File → Import → Upload and then select the movie 2.csv file that we downloaded from Kaggle.
I’ll name this spreadsheet “Movies”

First, we’ll look at the dataset to learn more about its structure. We’ll highlight all the cells and double click on the resize handle between the columns to adjust all column sizes. There are 7769 rows and 15 columns.

Belows are the list of all columns:
* `budget` (num): The budget of a movie. Some movies don't have this, so it appears as 0.
* `company` (txt): The production company
* `country` (txt): Country of origin
* `director` (txt): The director
* `genre` (txt): Main genre of the movie.
* `gross` (num): Revenue of the movie
* `name` (txt): Name of the movie
* `rating` (txt): Rating of the movie (R, PG, etc.)
* `released` (txt): Release date (YYYY-MM-DD)
* `runtime` (num): Duration of the movie
* `score` (num): IMDb user rating
* `votes` (num): Number of user votes
* `star` (txt): Main actor/actress
* `writer` (txt): Writer of the movie
* `year` (num): Year of release

The data type was confirmed by using the =ISNUMBER() and =ISTEXT() functions.

### Questions
1. What are the highest-earning movies ever, and how has their performance changed over time?
2. Have there been any shifts in genre popularity across different decades, and why might these changes have occurred?
3. Do certain types of movies tend to get better ratings from viewers, and how does this relate to their earnings?
4. How do different movie companies do in terms of earnings, and are there any clear trends?
5. Is there a connection between how much money is spent on marketing and how much a movie earns?
6. Do the writers and actors in movies affect viewer ratings and earnings?

### Objectives
1. Analyze historical movie performance trends and identify popular trends over time.
2. Investigate the factors contributing to the popularity of certain movies, including the roles of directors, actors, and genres.
3. Explore the evolution of genres across time periods and assess their implications for the movie industry.
4. Compare movie performance metrics across various countries to discern regional preferences and trends.
