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

First, we’ll look at the dataset to learn more about its structure. We’ll highlight all the cells and double click on the resize handle between the columns to adjust all column sizes. There are 7668 rows and 15 columns.

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

## Cleaning the data
- Freeze the header row and make it bold to make it easier to examine the data. 
- Remove whitespaces in all rows and columns by using the built-in function located under Data → Data cleanup → Trim whitespace. Then, ensure consistency in horizontal alignment by adjusting as needed to maintain uniformity. Align all number columns to the right and align the text columns to the left.

### Check for duplicates
We’ll detect duplicates by employing conditional formatting with the COUNTIF formula: =COUNTIF(A2:A7669, A2) > 1. Apply this formula by selecting the custom formula option under conditional formatting. 
![Screen Shot 2024-04-09 at 2 57 24 PM](https://github.com/ksadangrit/Movies/assets/156267785/d7d94b6a-1520-420c-8db3-884db0ff8eae)

To isolate duplicate entries, filter out non-highlighted rows and retain only duplicate rows. Achieve this by adding a filter and selecting Filter by color → Fill color → Magenta.

![Screen Shot 2024-04-09 at 2 58 29 PM](https://github.com/ksadangrit/Movies/assets/156267785/a9be2d1d-2a06-42c9-b3fe-ff573989ea6f)

Upon closely examining the flagged duplicate movie titles and comparing their release dates, it's apparent that they aren't true duplicates. Although certain movies share identical titles, they are distinct productions from separate years. Consequently, it's affirmed that all rows contain unique entries.

I’ll add the dollar sign for the budget and revenue columns and change the number format for the votes column to include commas for readability.

### Identifying missing values
To identify missing values (blank cells), apply a filter to the entire sheet and include only rows with blank cells or values synonymous with blank, such as 'unrated,' 'not rated,' or generic director terms without specific names.

In a new cell, use the` =SUBTOTAL(3, A:A)` formula to find out how many rows are missing certain information by counting the total rows from column A. Alternatively, you can use `=COUNTBLANK(L18:L7669)` to count the total blank column.

* `names` : No missing values
* `released` : 0.03% missing (2 rows with missing data)
* `rating` : 5.37% missing (412 not rated, unrated, and missing data)
* `genre` : No missing values
* `year` : 0.03% missing (2 rows with missing data)
* `score` : 0.04% missing (3 rows with missing data)
* `votes` : 0.04% missing (3 rows with missing data)
* `director` : 0.43% missing (33 rows with generic labels or missing data)
* `writer` : 0.04% missing (3 rows with missing data)
* `star` : 0.01% missing (1 row with missing data)
* `country` : 0.04% missing (3 rows with missing data)
* `budget` : 28% missing (2171 rows with missing data)
* `gross` : 2.47% missing (189 rows with missing data)
* `company` : 0.22% missing (17 rows with missing data)
* `runtime` : 0.05% missing (4 rows with missing data)

For columns with missing values less than 1%, I won't remove these rows altogether, as the small amount of missing data is unlikely to skew the findings or lead to inaccurate conclusions. However, with the `budget` column having over 28% of values missing, we'll investigate whether these missing values are evenly distributed among genres or if they are significant for certain genres. Additionally, we'll examine the gross of these movies to assess their impact on our findings.

To identify the number of rows with missing budget values for different genres, follow these steps:
- In cell S2, use the formula `=UNIQUE(C2:C7669)` to extract all genre names.
- Filter out rows without blank cells for budget. In column Q, enter the formula `=SUBTOTAL(103,C18)` from the first row to the last.
- Unfilter the sheet. In cell R2, use the formula `=SUBTOTAL(103,C18)` to determine the number of movies in each genre with blank cells.
- Additionally, calculate the total number of movies for each genre using the formula `=COUNTIF(C2:C7669, S2)` in cell T2, then drag the filter button down to the last genre.

It's noticeable that in certain genres with only a few movies, the absence of budget data constitutes 100% of the entries. However, even in genres with thousands of movies, the percentage of entries with missing budget data ranges from 16% to 42%. These percentages are significant, indicating that the lack of budget data isn't limited to specific genres. 

Furthermore, when examining the gross earnings from the rows with missing budget values, it becomes evident that over half of them generate revenue exceeding $1 million, with some top movies generating close to $1 billion. These figures are substantial, highlighting that eliminating movies with missing values would result in misleading conclusions. Therefore, the best approach for handling missing values is to impute them.

We'll also impute the missing values in the `gross` column, even though they only account for 2.47% of the dataset. This will be beneficial for our analysis to do so as these columns are typically used together for calculations and analyses, particularly in assessing profitability.
