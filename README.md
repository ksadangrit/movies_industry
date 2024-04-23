# Movies
![pexels-tima-miroshnichenko-7991579](https://github.com/ksadangrit/Movies/assets/156267785/48e0806f-548b-43d7-98df-ffd9d420c4ff)

_Photo by Tima Miroshnichenko from [Pexels](https://www.pexels.com/photo/cartoon-movie-showing-on-theater-screen-7991579/)_

## Introduction
This case study aims to explore the dynamics of the film industry and the evolving trends across different decades and years. As a movie enthusiast, I find it captivating to delve into the timeless classics of each genre and understand the preferences of moviegoers. Furthermore, I anticipate that this study will offer valuable insights into the movie business, shedding light on the factors contributing to the success of films in terms of both profitability and audience reception. Such insights will undoubtedly benefit aspiring filmmakers, actors, and production companies.

This dataset is scrapped from IMDb by Daniel Grijalva and is available to download on [Kaggle](https://www.kaggle.com/datasets/danielgrijalvas/movies). The dataset contains information about movies from between 1980 - 2020.

Click here for the [license](https://creativecommons.org/publicdomain/zero/1.0/).

### Questions
1. What are the highest-earning movies of all time and in each decade?
2. Have genre popularity shifted across different decades?
3. How does the origin of movies affect their performance?
4. Which factors strongly influence movie performance?
5. Is there a positive correlation between budgets and revenues?


### Objectives
1. Analyze historical movie performance trends and identify popular trends over time.
2. Investigate the factors contributing to the popularity and performance of movies, including the roles of directors, actors, and genres.
3. Explore the evolution of genres across time periods and assess their implications for the movie industry.
4. Compare movie performance metrics across various countries to discern regional preferences and trends.

### Analysis Workflow
* Importing data
* Cleaning the data
* Calculations, Analysis, and Visualizations
* Key Findings and Recommendations

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

The data type was confirmed by using the `=ISNUMBER()` and `=ISTEXT()` functions.

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

## Calculations, Analysis, and Visualizations
In this phase of the project, I'll primarily utilize pivot tables for data manipulation and will complement the analysis with charts and graphs to visually present the findings. Significant insights will be highlighted and discussed.

### Decades
#### Creating a decade column
- We’ll add a decade column next to `year` by right-clicking on the 'year' column.
- Select 'Insert 1 column right.'
- Name the new column 'Decade' in cell E2.
- Enter the formula '=TEXT(INT(D2/10)*10, "0") & "s"' in cell E2.
- Double-click on the blue filter button to apply the formula to the entire column.

#### Revenues by decade
We'll create a pivot table to summarise average revenue, total revenue, minimum, and maximum revenue by decade, taking into account that the 2020s decade only includes the year 2020.

![Screen Shot 2024-04-17 at 10 31 56 AM](https://github.com/ksadangrit/movies/assets/156267785/c7cd5723-287d-4aaa-ab68-8edd933d7b5e)

- Highlight all the columns in the movies sheet.
- Select 'Insert' → 'Pivot table' → 'New sheet'.
- Drag ‘decade' into the 'Rows' section. Under 'Summarized by', select 'COUNT'.
- Drag 'name' into the 'Values' section four times. For each instance, select 'AVERAGE', 'SUM', 'MIN', and 'MAX' under 'Summarized by'.
- Apply conditional formatting to the 'Total revenue' and 'MAX of revenue' columns. Choose a gradient from white to deep orange, with deeper colors indicating higher values, to visually highlight and differentiate the range of values.

#### Finding movies with highest revenue for each decade
The movie names from the movie sheet are in the leftmost column, so the VLOOKUP function can't be used. Instead, we’ll utilize `INDEX` and `MATCH` functions for this task.
- Input the formula `=INDEX(movies!A:A, MATCH(F2, movies!N:N, 0))` in cell F2.
- Double-click the blue button to autofill the remaining cells.

![Screen Shot 2024-04-17 at 10 35 30 AM](https://github.com/ksadangrit/movies/assets/156267785/2fcf765b-0022-40db-bd81-03099d2f71c1)

**Findings**

- The average revenue for a movie is $77 million, and this figure has consistently increased from the 1980s to the 2020s.
- Notable top-grossing films include "E.T.," "Titanic," "Avatar," "Avengers: Endgame," and "The Eight Hundred" for the 1980s, 1990s, 2000s, 2010s, and 2020s, respectively.
- While it may appear that movies are not performing well in the 2020s, this is likely due to the incomplete dataset for the decade. However, based on average revenue trends, the total revenue for the 2020s is expected to surpass that of all previous decades.

### Top 5 Movies of All Time 
- To rank all movies, we'll first copy the `name`, `budget`, and `revenue` columns into a new sheet. Since there are multiple movies with the same names, we cannot use a pivot table to summarise the data
- Next, we'll create a new column called `profit`. In cell D2, enter the formula `=C2-B2`, then double-click the blue button to autofill the rest of the column.
- Finally, we'll apply a filter to the entire sheet and rank the movies based on total revenue and total profit.
- Highlight the top 5 rows of movies and insert a bar chart.

![Top 5 Movies by Revenue ](https://github.com/ksadangrit/movies/assets/156267785/f4181f31-4f0b-45b6-a55a-74cc7c8d4ff4)

**Findings**
- Avatar leads as the highest-grossing movie of all time, followed by Avengers: Endgame, Titanic, Star Wars, and Avengers: Infinity War.
- The top three movies also hold the record for the highest revenue from the 1990s to the 2010s.
- Similarly, the top five movies are consistent when ranked by profit.
- Despite their high budgets, these blockbuster movies yield massive profits.

### Scores and Votes
### Top 5 Movies by Total Scores and Number of Votes
We'll replicate the process from previous sections by copying and pasting the relevant columns, sorting them based on scores and votes using filters, and then selecting the desired rows and columns to create a chart.

| Total scores                           | Total votes                       |
| ------------------------------------- | ----------------------------------------------- |
| ![Top 5 Movies by IMDb score](https://github.com/ksadangrit/movies/assets/156267785/7eee09c4-c124-447b-8bc9-b04afdfda736)| ![Top 5 Movies by Number of Votes](https://github.com/ksadangrit/movies/assets/156267785/b83984a9-8dd3-43de-a336-80634712c120)|

**Findings**
- The Shawshank Redemption leads with the highest number of votes and the highest scores, followed closely by The Dark Knight.
- While Pulp Fiction, The Lord of the Rings: The Return of the King, and Schindler's List share a rating of 8.9, only Pulp Fiction ranks in the top 5 most voted.
- Each movie in the top 5 most voted received over 1.9 million votes, and three out of five also received the highest ratings. This suggests that these movies left a significant positive impression on the audience, prompting them to take the time to vote.

### Companies
### Top 5 Companies by Average Revenue and Average Profit
- Highlight the `company`, `budget`, and `revenue` columns in the `movies` sheet, then select "Insert" --> "Pivot table" into a new sheet.
- In the new sheet, drag `company` to rows and `revenue` to values.
- Add a calculated field under values with the formula `=AVERAGE('revenue')-AVERAGE('budget')` to find the average profit.
- Apply filter to sort the company based on revenue and profit.
- Highlight the top 5 rows and insert a chart.

| Average Revenue                      | Average Profit                  |
| ------------------------------------- | ----------------------------------------------- |
| ![Top 5 Companies by Average Revenue](https://github.com/ksadangrit/movies/assets/156267785/f845c466-73d1-4042-bfee-2c26dc156393)| ![Top 5 companies by Average Profit (1)](https://github.com/ksadangrit/movies/assets/156267785/cec65cd6-bb51-4208-bb40-21a8eb11ec5f)|

**Findings**
- Marvel Studios tops both lists as the company with the highest profits and gross earnings, followed by Illumination Entertainment, Fairview Entertainment, and B24.
- Chris Morgan ranks fifth for profits but doesn't appear on the list for average revenue. This disparity could be due to significant differences in budget and revenue for their movies.
- Avi Arad Productions' movies outperform Chris Morgan's in terms of gross revenue.

### Actors
### Top 5 Actors by Total Movies and Total Revenue
I chose to compare the top 5 actors based on both the total number of movies they've starred in and the cumulative revenues of those movies. This comparison aims to explore whether actors' longevity in the industry correlates with the success of their movies or if other factors play a more significant role in determining movie success. 

We use a pivot table to summarise the total number of movies and total revenue, sorting them accordingly before inserting a chart.

| Total Movies                      | Total Revenue                  |
| ------------------------------------- | ----------------------------------------------- |
| ![Top 5 Actors based on Number of Movies](https://github.com/ksadangrit/movies/assets/156267785/4b5ea5b9-1083-4b20-afbb-43536152a74e)| ![Top 5 Actors based on Movie Revenues](https://github.com/ksadangrit/movies/assets/156267785/166c6e98-13f3-4f68-bdc8-fff244cd41a8)|

**Findings**

- Tom Hanks and Tom Cruise are the only two actors who appear on both lists, indicating their enduring popularity and significant impact on movie revenues.
- Nicolas Cage has the highest number of movie appearances, and Denzel Washington ranks fourth in terms of appearances. However, their overall movie revenues do not place them in the top 5.
- Conversely, Robert Downey Jr. generated the highest total revenues, while Will Smith ranks fifth. This underscores their box office success despite fewer movie appearances.
- All these actors have lengthy careers in the industry, suggesting a correlation between longevity and movie success.

### Directors
### Top 5 Directors by Total Movies and Total Revenue
Similarly to actors, we'll rank top 5 directors based on the number of movies and total revenue. Pivot table is still used for summatization and calculation.

| Total Movies                      | Total Revenue                  |
| ------------------------------------- | ----------------------------------------------- |
|![Top 5 Directors by Total Revenue (1)](https://github.com/ksadangrit/movies/assets/156267785/8015a69f-4600-4ebc-bd11-95e2512480a0) | ![Top 5 Directors by Total Movies (1)](https://github.com/ksadangrit/movies/assets/156267785/657d4256-47ca-4028-90af-aec491a0f0d5)|

**Findings**
- Steven Spielberg is the only director who appears on both lists, ranking first for total revenue.
- None of the other top 5 directors based on total revenue are in the top 5 for total number of movies, and vice versa.
- The influence of directors on film success is evident, with all top 5 directors being well-known and experienced.
- While not as significant as that of actors, their prominence likely contributes to the films' success.
- However, directing numerous films doesn't necessarily indicate popularity, as directors typically initiate projects and secure budgets, unlike actors who are hired.

### Writers
### Top 5 Writers by Total Movies and Total Revenue
We'll repeat the process from previous section to rank top 5 writer using the `writer`, `name` and `revenue` columns.

| Total Movies                      | Total Revenue                  |
| ------------------------------------- | ----------------------------------------------- |
| ![Top 5 Writers by Total Movies](https://github.com/ksadangrit/movies/assets/156267785/928f7929-3a38-453e-ba37-61f2d679605e)| ![Top 5 Writer by Total Revenue](https://github.com/ksadangrit/movies/assets/156267785/7a28b3ba-814e-4657-87e4-a4d7dd1886fb)|

**Findings**

- In terms of total movies, the writer with the most is Woody Allen, followed by Stephen King.
- On the other hand, the movies written by Christopher Markus generated the most total revenue, followed by James Cameron's.
- These two top 5 lists do not share the same writers. This suggests that, compared to directors and actors, writers do not strongly influence the success of films. It also suggests that other factors play bigger roles in whether a movie is going to be successful.
  
### Countries
### Top 5 Countries by Total Movies and Median Revenue
For this section, we'll utilize pivot tables to summarise the total number of movies, percentage, and median revenue. 

Instead of average revenue, we'll focus on median revenue to mitigate the skewing effect caused by the dominance of the USA in the movie industry, as observed in previous sections where top-grossing movies primarily originated from the USA.

| Total Movies                      | Median Revenue                  |
| ------------------------------------- | ----------------------------------------------- |
| ![chart (1)](https://github.com/ksadangrit/movies/assets/156267785/2d28db99-3154-42da-bd3d-b62db3242cb6)| ![Top 5 Countries by Median Revenue (1)](https://github.com/ksadangrit/movies/assets/156267785/75f63692-9484-4135-8e58-78127c59a84a)|

**Findings**
- The USA leads with over 5,000 movies, comprising over 70% of all films, followed by the UK at 11%, and France, Canada, and Germany.
- However, each country in the top 5 for median revenue represents less than 1.5% of all movies released.
- This discrepancy may be due to the varied performance of movies released by countries like the USA and the UK.
- Non-English speaking countries dominate the top spots for median revenue, indicating international success.

### Months
#### Extracting the month from the `released` column
We'll extract the month each movie was released using the `LEFT` and `FIND` functions by following these steps:
- In cell Q2, enter the formula `=LEFT(F2, FIND(" ", F2) - 1)`. This formula finds the month name, which is the leftmost text before the first space.
- Pivot table will be created to summarise the month and number of movies released during each month.
- There are 9 movies with missing month details, accounting for about 0.1% of all data.
- We'll disregard these missing values because even if we replace them with the mode, which is October, the result won’t change.
- To arrange the months from January to December for charting purposes, I'll copy and paste the summarised values and adjust the order accordingly. 
- Additionally, I’ll apply a color scale to both the average revenue and total movies columns to better highlight their performances.

![Screen Shot 2024-04-17 at 12 43 05 PM](https://github.com/ksadangrit/movies/assets/156267785/9a65d7ca-33fa-4fdf-bd42-8a6974cc2cfb)

**Findings**

- Movies were released most frequently in October, followed by August and March.
- On average, movies earned the highest revenue during May to July and November to December.
- There is a notable contrast between the total number of movies released in a month and the gross revenue. This suggests that movies may tend to earn more when there are fewer competitors.
- December is the second highest-grossing month. This could be attributed to holiday movies released during December, which tend to generate higher revenue compared to other months.

### Genres
### Rank Genres by Average Profit
We'll still utilise pivot table to summarise the average profit generated for each genre and then insert a bar chart to visualise the result.

![Average Profit by Genre](https://github.com/ksadangrit/movies/assets/156267785/fe4fd988-9dca-4731-b36e-5b5730a9c97d)

**Findings**

- Animation leads as the genre with the highest average profit, surpassing $200 million, closely followed by family.
- Action, adventure, and mystery genres also demonstrate strong commercial performance.
- Conversely, music, musical, and sports genres tend to underperform financially, with movies in these genres more likely to incur losses.

### Number of Movies by Genre and Year
We'll insert a pivot table, with genre in Rows, year in Columns, and Name in Values summarized by COUNTA. Then, we'll visualize the trends using a line chart.

![Total Number of Movies by Genre](https://github.com/ksadangrit/movies/assets/156267785/9f592b36-8b42-49c6-993f-26cd310d2c79)

**Findings**

- Comedy, action, and drama movies experienced an initial surge starting in the early 1980s, continuing until the late 1990s with a slight decline.
- Comedy movies dominated production until the 2010s when the action genre gained popularity, followed by drama.
- Horror movies saw a notable increase, particularly in the latter part of the 2010s.
- Other genres typically had fewer than 25 movies produced per year, indicating lower popularity compared to comedy, action, drama, and horror genres.

### Genres vs Scores
We'll analyze the relationship between IMDb scores, total movie counts, and votes to identify any correlations. Using pivot tables, we'll calculate sum and average values for comparison.

![Screen Shot 2024-04-19 at 12 01 23 AM](https://github.com/ksadangrit/movies/assets/156267785/feb3706d-e796-4e4a-8d9a-57d72d776902)

**Findings**

- Music and musical genres have the highest average scores at 8.1 and 7.2, respectively.
- Despite having only one movie in the music genre, it garnered 12,000 votes, indicating its popularity.
- Genres like mystery, action, adventure, and animation received over 100,000 votes each, showing their widespread appeal.
- Most genres received scores above 6, but horror, sport, thriller, and western received comparatively lower ratings.

### Ratings
We'll compare movie counts and average revenues across different ratings using pivot tables and visualize the results with pie and bar charts.

| Total Movies                      | Average Revenue                  |
| ------------------------------------- | ----------------------------------------------- |
| ![Number of movies by rating  (1)](https://github.com/ksadangrit/movies/assets/156267785/6968c6c2-2f23-4f23-9042-0c38025a41c3)|![Average Revenue vs  Rating](https://github.com/ksadangrit/movies/assets/156267785/f5f08ca1-86d1-44e4-81f2-259dd45ddfa2)|

**Findings**

- R is the most common rating, followed by PG and PG-13, collectively representing over 93% of all movies.
- This indicates a trend toward broader audience appeal rather than restricting content to adult-only audiences.
- Movies with ratings like G, PG-13, and PG tend to generate higher revenues, possibly due to their accessibility to wider audience demographics, including families with children or teenagers.

### Average Budget vs Revenue over the Years
We'll compare the average budget and revenue over the years by using pivot table to summarize the data then inserting a line chart to illustrate the results.

![Average Budget vs Revenue by Year](https://github.com/ksadangrit/movies/assets/156267785/59344866-f799-4fff-a7e2-a4fa84126654)

**Findings**

- On average, movie profits have surged over the years, despite a gradual increase in movie budgets.
- Average revenue has also grown steadily since the 2000s, even though there hasn't been a significant increase in average budgets.
- This suggests a positive correlation between budget and revenue.

### Budget vs Revenue
For this section, we'll copy and paste the `movie`, `budget` and `revenue` columns into a new sheet. We'll highlight those column and insert a scatterplot to examine any correlation between the two.

![Budget vs Revnue](https://github.com/ksadangrit/movies/assets/156267785/1af1b7bb-d291-4f0f-8223-851c47fbab5d)

**Findings**

- A cluster of movies with budgets under $150 million and revenues under $1 million dollar is evident.
- While there are some movies with high budgets that did not perform well at the box office, there are no instances of movies with revenues between $2-3 billion having budgets lower than $200 million.
- The scatterplot suggests a positive correlation between movie budgets and revenues, indicating that higher budget films tend to generate higher revenues.

### IMDb scores vs Revenue
We'll repeat the process from the previous scatterplot, this time analyzing the relationship between IMDb scores and revenue.

![IMDb Scores vs Revenue](https://github.com/ksadangrit/movies/assets/156267785/e941cf33-20cb-4a33-8a49-539a841e1cf5)

**Findings**

- There is a range of movies with revenue under $500k that have IMDb scores ranging from 2 to over 9.
- Except for one outlier, all movies that generate over $1 billion score above 6 on IMDb.
- There exists a positive correlation between movie revenue and IMDb scores, particularly evident when movies earn over $1 billion, indicating that financially successful movies tend to receive positive reviews from audiences.

### Number of Votes vs IMDb scores
We'll repeat the process from the previous scatterplot, this time analyzing the relationship between votes, and IMDb scores.

![Votes vs IMDb scores](https://github.com/ksadangrit/movies/assets/156267785/1bbfc775-3d74-412e-aac7-fd45dabf253d)

**Findings**

- Most movies receive fewer than 500,000 votes.
- Higher-voted movies tend to have narrower score ranges, typically around 8 or higher for those with over 1 million votes.
- The data suggests that movies with extensive audience engagement tend to receive more positive ratings.

### Runtime vs IMDb scores
We'll follow the same steps as before to analyze the correlation between movie runtime and IMDb scores using a scatterplot.

![Runtime vs IMDb score](https://github.com/ksadangrit/movies/assets/156267785/9c07012d-25da-4c51-ab96-1a5f4aa4f9fc)

**Findings**

- Movies with runtimes under 150 minutes exhibit a broad range of IMDb scores, spanning from around 2 to over 8.
- Conversely, films with runtimes exceeding 180 minutes consistently receive scores above 6, suggesting a positive correlation between longer runtimes and higher IMDb ratings.

## Key Findings and Recommendations

### Summary of Key Findings
- Average budget and revenue have increased over decades and years.
- Revenue has consistently risen in each decade from the 1980s to the 2010s.
- Titanic, Avatar, and Avengers: Endgame are top-grossing movies for their respective decades and all-time.
- Comedy, Action, and Drama are popular genres, with Comedy's popularity declining after the 2000s.
- Animation and Family genres yield the highest profits, while niche genres like Sport and Western tend to suffer losses.
- Positive correlation exists between IMDb scores and votes, revenue, and runtime, particularly with higher values.
- Family-friendly ratings (PG, G, PG-13) are common and tend to perform better at the box office.
- Actors have more influence on film success than directors, evidenced by correlations between top actors and movie revenue.
- Writers have minimal impact on movie success.
- Most movies come from English-speaking countries, with the USA dominating. However, countries producing fewer movies see higher median revenue.
- Movies released in June and December generate the most revenue, suggesting fewer releases at those times lead to better performance.
- Companies producing movies with the highest average revenue also boast the highest profits.
- Overall, successful films positively impact the popularity of genres, actors, directors, writers, and company performance, evidenced by the rise of action and superhero movies, as well as animations.

### Recommendations
- Filmmakers and companies should carefully allocate budgets, prioritize profitable genres, and manage costs in niche markets.
- To maximize revenue potential, choose release dates when competition is low to enhance box office performance.
- Further study could focus on analyzing audience demographics and preferences to better understand the factors driving film success and tailor content accordingly.
