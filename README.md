# Movies
![pexels-tima-miroshnichenko-7991579](https://github.com/ksadangrit/Movies/assets/156267785/48e0806f-548b-43d7-98df-ffd9d420c4ff)

_Photo by Tima Miroshnichenko from [Pexels](https://www.pexels.com/photo/cartoon-movie-showing-on-theater-screen-7991579/)_

## Introduction
This case study aims to explore the dynamics of the film industry and the evolving trends across different decades. As a movie enthusiast, I find it captivating to delve into the timeless classics of each genre and understand the preferences of moviegoers. Furthermore, I anticipate that this study will offer valuable insights into the movie business, shedding light on the factors contributing to the success of films in terms of both profitability and audience reception. Such insights will undoubtedly benefit aspiring filmmakers, actors, and production companies.

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
* `revenue` (num): Revenue of the movie
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
- Rename the `gross` column to `revenue` for clarity and to avoid confusion.
- Remove whitespaces in all rows and columns by using the built-in function located under Data → Data cleanup → Trim whitespace. Then, ensure consistency in horizontal alignment by adjusting as needed to maintain uniformity. Align all number columns to the right and align the text columns to the left.

### Check for duplicates
We’ll detect duplicates by employing conditional formatting with the COUNTIF formula: =COUNTIF(A2:A7669, A2) > 1. Apply this formula by selecting the custom formula option under conditional formatting. 
![Screen Shot 2024-04-09 at 2 57 24 PM](https://github.com/ksadangrit/Movies/assets/156267785/d7d94b6a-1520-420c-8db3-884db0ff8eae)

To isolate duplicate entries, filter out non-highlighted rows and retain only duplicate rows. Achieve this by adding a filter and selecting Filter by color → Fill color → Magenta.

![Screen Shot 2024-04-09 at 2 58 29 PM](https://github.com/ksadangrit/Movies/assets/156267785/a9be2d1d-2a06-42c9-b3fe-ff573989ea6f)

Upon closely examining the flagged duplicate movie titles and comparing their release dates, it's apparent that they aren't true duplicates. Although certain movies share identical titles, they are distinct productions from separate years. Consequently, it's affirmed that all rows contain unique entries.

I’ll add the dollar sign for the budget and revenue columns and change the number format for the votes column to include commas for readability.

### Identifying missing values
To identify missing values (blank cells), apply a filter to the entire sheet and include only rows with blank cells.

In a new cell, use the` =SUBTOTAL(3, A:A)` formula to find out how many rows are missing certain information by counting the total rows from column A. Alternatively, you can use `=COUNTBLANK(L18:L7669)` to count the total blank column.

* `names` : No missing values
* `released` : 0.03% missing (2 rows with missing data)
* `rating` : 1% missing (77 rows with missing data)
* `genre` : No missing values
* `year` : No missing values
* `score` : 0.04% missing (3 rows with missing data)
* `votes` : 0.04% missing (3 rows with missing data)
* `director` : No missing values (31 rows with generic labels)
* `writer` : 0.04% missing (3 rows with missing data)
* `star` : 0.01% missing (1 row with missing data)
* `country` : 0.04% missing (3 rows with missing data)
* `budget` : 28% missing (2171 rows with missing data)
* `revenue` : 2.47% missing (189 rows with missing data)
* `company` : 0.22% missing (17 rows with missing data)
* `runtime` : 0.05% missing (4 rows with missing data)

For columns where missing values constitute less than 1% of the data, I plan to drop rows containing those missing values. Given that many of these rows have multiple missing values, particularly in important columns like `budget` and `revenue`, their removal is unlikely to lead to misleading conclusions as they are relatively insignificant.

However, in the case of the `budget` column, which has over 28% of values missing, further investigation is warranted. We will explore whether these missing values are evenly distributed among genres or if they are more prevalent in certain genres. Additionally, we will analyze the revenue earnings of these movies to understand their potential impact on our findings. 

Similarly, although the `rating` column has just around 1% of rows with missing values, many of these movies have high revenue earnings, which could significantly affect our overall data if we were to drop them. Therefore, we will explore alternative solutions for handling missing values in this column.

### Dropping rows 
I'll go through each column, excluding those with no missing values and those requiring further investigation as mentioned, and proceed with the following steps:

![Screen Shot 2024-04-11 at 4 09 13 PM](https://github.com/ksadangrit/Movies/assets/156267785/5d485163-0a83-4046-93a2-bcb65924d2b7)

- Apply a filter to the entire sheet and retain only the rows with blank cells.
- Delete those rows.
- Repeat the above steps for all columns

At the conclusion of this process, we will have 7,643 movies remaining in total.

### Investigating the Distribution of Rows with Missing Budget Values Across Genres
To identify the number of rows with missing budget values for different genres, follow these steps:
- In cell T2, use the formula `=UNIQUE(C2:C7669)` to extract all genre names.
- Filter out rows without blank cells for budget. In column R, enter the formula `=SUBTOTAL(103,C18)` from the first row to the last 
- Unfilter the sheet. In cell S2, use the formula `=COUNTIFS(C$2:C$7646,T2,R$2:R$7646,"=1")` to determine the number of movies in each genre with blank cells.
- Additionally, calculate the total number of movies for each genre using the formula `=COUNTIF(C2:C7669, T2)` in cell U2, then drag the filter button down to the last genre.
- In cell V2, calculate a percentage using this formula `=S2/U2*100` and drag the filter button down to the last genre.

![Screen Shot 2024-04-11 at 12 23 50 PM](https://github.com/ksadangrit/Movies/assets/156267785/3d960b24-fcb4-4f8e-948f-83e7ee1d8a7a)

It's noticeable that in certain genres with only a few movies, the absence of budget data constitutes 100% of the entries. However, even in genres with thousands of movies, the percentage of entries with missing budget data ranges from 16% to 42%. These percentages are significant, indicating that the lack of budget data isn't limited to specific genres. 

Furthermore, when examining the revenue earnings from the rows with missing budget values, it becomes evident that over half of them generate revenue exceeding $1 million, with some top movies generating close to $1 billion. These figures are substantial, highlighting that eliminating movies with missing values would result in misleading conclusions. Therefore, the best approach for handling these missing values is to impute them.

We'll also impute the missing values in the `revenue` column, even though they only account for 2.47% of the dataset. This will be beneficial for our analysis to do so as these columns are typically used together for calculations and analyses, particularly in assessing profitability.

### Creating a box plot for data distribution:
We'll construct a box plot based on the five-number summary. Although Google Sheets doesn't require the median for a box plot, we'll calculate both the mean and median for comparison.
1. Filter out blank cells in the 'budget' column.
2. Copy and paste values only into a new sheet.
3. In columns B to G, calculate the MIN, Quartile 1, Quartile 3, MAX, Median, and Mean, respectively.
4. Highlight the values in columns A (budget) through E in the first row.
5. Insert → Chart → Under Chart type, select 'Candlestick chart'.

![Screen Shot 2024-04-12 at 11 31 38 AM](https://github.com/ksadangrit/Movies/assets/156267785/c235b612-a67d-464c-b2ee-b43f88f83d0f)

Based on the resulting plot, we observe a right or bottom skew in the data, indicating a few movies with very high budgets that influence the mean and maximum values.

**Imputation Method:** In this scenario, imputing missing data with **the median** is more appropriate. The median is less sensitive to outliers and provides a more robust measure in the presence of skewness, offering a better reflection of the typical budget for movies in the dataset.

We'll repeat steps 1 to 5 for the `revenue` column to determine the most appropriate imputation method.

![Screen Shot 2024-04-12 at 11 35 58 AM](https://github.com/ksadangrit/Movies/assets/156267785/74aa23a7-3fe0-41fd-807d-9adf60534b82)

The plot shows a similar pattern to the budget plot, indicating a pronounced right skew caused by a handful of movies with exceptionally high revenues. The maximum revenue exceeds $2.8 billion, and the mean exceeds the median by over $50 million. Therefore, the most suitable approach for imputing missing values is to use the median.

We'll replace all blank cells in the `budget` column with the median value, which is $21,000,000, by following these steps:

![Screen Shot 2024-04-12 at 11 43 32 AM](https://github.com/ksadangrit/Movies/assets/156267785/6f05bc1a-843f-4e1b-a568-48f00bcac7a6)

- Highlight the column and select 'Find and replace' under the 'Edit' menu.
- In the 'Find' box, use '^\s*$' to find blank cells, and tick both 'Match case' and 'Search using regular expressions'.
- Enter the median value to replace with.
- Select 'Replace all'.

We'll repeat the same process to replace blank cells in the `revenue` column with $20,240,315.

### Replacing blank cells in the `rating` column with the mode
We'll determine the mode of all values in the `rating` column by following these steps:
- In a new sheet, enter this formula in cell A1: `=UNIQUE(FILTER(movies!B:B, movies!B:B<>""))`. This will extract all unique values, excluding blank cells, from the movies sheet.
- In cell B2, count frequencies using this formula: `=COUNTIF(movies!B:B, A2)`. Double-click the filter button for the other numbers to show up.
- Use the `INDEX` and `MATCH` functions in this formula: `=INDEX(A2:A, MATCH(MAX(B2:B), B2:B, 0))` to find the mode from all rating types.
  
![Screen Shot 2024-04-12 at 1 54 10 PM](https://github.com/ksadangrit/Movies/assets/156267785/300a7e97-42fc-46ac-b12e-3f2c84e9d592)

The result shows that "R" is the most common rating and is the mode from the `rating` column. We'll replace all the blank cells in this column with "R" using the Find and Replace option, the same way we did earlier.

### Calculations and Analysing


