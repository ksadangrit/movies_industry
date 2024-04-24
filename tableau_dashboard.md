# Tableau Dashboard for Movie Data

**Tools:** I utilized **Tableau** for importing data and creating charts, and **Canva** for the background image.

I have chosen to employ Tableau to develop an interactive dashboard, providing deeper insights into the film industry. This includes filter options for specific genres and decades. The charts I created are as follows:

- Average Budget vs. Revenue
- Total Movies by Country
- Top 5 Movies by Revenue and IMDb Scores
- Top 5 Directors, Actors, and Companies

I accomplished this through the following steps:

1. Connected the cleaned dataset from Google Sheets to Tableau.
2. Created a new worksheet.
Established a new `Calculated Field` named "Top 5" using the formula `index()<=5`. This formula ensures that only five data points are displayed in the chart.

   2.1 Horizontal Bar Chart for Top 5 Movies by IMDb Scores and Revenues
   - Created a `Calculated Field` named "Name_Year" using the formula `([Name] + " - " + STR([Year]))` to ensure unique values for names and years.
   - Plotted `Revenue` or `Score` against `Name_Year` and applied filters for `Genre`, `Decade`, and `Top 5`.
   - Used `Name` for color and sorted the chart in descending order.
   
   2.2 Vertical Bar Chart for Top 5 Actors and Directors
   - Plotted `Director` or `Actors` against `Revenue`, applied filters, and sorted the sheet in descending order.
   
   2.3 Top 5 Companies
   - Utilized a square chart to represent the top 5 companies, with `Company` on rows and `Revenue` (summed) on color and label. Applied filters accordingly.
   
   2.4 Budget vs. Revenue (Line Chart)
   - Plotted `Year` against `Revenue` and `Budget` with average as the measure for both. Applied filters and used `Genre` for additional filtering.
   
   2.5 Average Revenue, Runtime, and IMDb Scores
   - Employed text visualizations by directly dragging `Revenue` to text and ensuring average as the measure. Applied filters for `Genre` and `Decade`.
   
   2.6 Total Movies by Country (Map)
   - Mapped `Country` to details and `Name_Year` to color, selecting "Count (Distinct)" as the measure and "Sunrise-Sunset Diverging" as the palette.

4. Dashboard Design
   - Designed the dashboard background using Canva and incorporated it into the Tableau dashboard. Added all charts and filters accordingly.

The end result is an interactive dashboard offering comprehensive insights into the movie industry.

<div class='tableauPlaceholder' id='viz1713920516664' style='position: relative'><noscript><a href='#'><img alt='Dashboard 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Fi&#47;FilmIndustry_17137504642190&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='FilmIndustry_17137504642190&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Fi&#47;FilmIndustry_17137504642190&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-GB' /></object></div> 


To view the full dashboard on Tableau, click [here](https://public.tableau.com/views/FilmIndustry_17137504642190/Dashboard1?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link). 
