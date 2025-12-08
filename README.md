Power BI – COVID-19 Analytics Dashboard (Cumulative & Daily Case Trends)
Power BI dashboard for analyzing the evolution of COVID-19 cases worldwide.
Cumulative case data is transformed into daily cases and time-intelligence metrics to track outbreaks, growth, and decline periods, with drillthrough views by country.

1. Project Overview
This project builds an end-to-end analytical report in Power BI using public COVID-19 case data.
The goal is to turn raw cumulative case numbers into an interactive analytics dashboard that allows you to:
•	Monitor the global impact of the pandemic.
•	Compare confirmed cases over time.
•	Detect waves, outbreaks, and recovery periods.
•	Explore detailed trends for each country through drillthrough.
The model applies star-schema modeling, calendar tables, and DAX measures to calculate daily cases, yearly totals, month-over-month changes, year-over-year (YoY) growth, and monthly YoY variation.

2. Main Features
Overview Page – Global View
•	Top 5 Country Yearly Cases (Treemap)
Highlights the countries with the highest confirmed cases in the selected year.
•	Cumulative Case Trend (Line Chart)
Shows the evolution of total confirmed cases over time, segmented by year and driven by the calendar table.
•	Global Impact Rank (Table)
Ranks countries by total cases and shows:
o	Total cases
o	YoY change (absolute variation vs previous year)
o	YoY growth % (relative variation vs previous year)
o	Days with zero cases (for additional context on control or reporting gaps)
•	Year and Country Slicers
o	Year selector to focus on a specific period.
o	Country selector used to enable and drive drillthrough to the detailed page.
This page is intentionally kept at a high level: it is designed for global monitoring and comparison, without country-specific KPIs in the header.
3. Country Details Page – Drillthrough View
When the user right-clicks a country in the overview table and selects “Drillthrough”, a country-level analytics page is displayed.
KPI Cards (Latest Year Context)
•	Country/Region – Selected country context.
•	Cumulative Confirmed Cases – Total cases for the selected country.
•	Last Reported Year Cases – Yearly cases for the most recent year with data.
•	Zero-Case Days (Latest Year) – Number of days with zero reported cases in the latest year (useful to understand spread control and reporting density).
Visuals
1.	Daily Covid-19 Cases (Historical Evolution)
Line chart showing daily cases over the full timeline (Year → Quarter → Month → Day).
Used to identify waves, peaks, and decline periods in a single country.
2.	Monthly Year-over-Year Case Variation (%)
Column chart plotting the percentage change in cases compared to the same month in the previous year.
o	Positive values (red) indicate higher cases than the previous year (worse situation).
o	Negative values (blue) indicate fewer cases (improvement).
This helps explain why the curve moves, not just how much.
3.	Annual Confirmed Cases Comparison
Column chart with yearly totals, allowing quick comparison of the intensity of each wave at the annual level.
4.	Monthly Distribution by Year (Heatmap)
Matrix/heatmap of Year × Month with color-coded case intensity.
Useful for spotting seasonal patterns, key outbreak months and recovery periods.

4. Data Model and DAX
Data Model
•	Fact table with cumulative confirmed cases by date and country.
•	Date dimension (Calendar table) with:
o	Date
o	Year
o	Quarter
o	Month
o	Year-Month
o	Other derived attributes for time intelligence.
•	Country dimension (implicit in the COVID fact table).
The model follows a star-schema approach to keep relationships simple and optimized for DAX.
Key Measures (Examples)
Some of the measures used in the report include:
•	Daily Cases – Difference in cumulative cases vs previous day.
•	Yearly Cases – Sum of Daily Cases over the selected year (using DATESYTD).
•	Cases Last Year – Shifts the context one year back using DATEADD.
•	YoY Change – Absolute difference between Yearly Cases and Cases Last Year.
•	YoY Growth % – Relative variation using DIVIDE( [YoY Change], [Cases Last Year] ).
•	Monthly Cases – Monthly accumulation based on the date context.
•	Monthly YoY % Change – YoY variation at Year-Month grain, with logic to avoid infinite growth from zero-case months.
•	Days with Zero Cases – Counts days where Daily Cases = 0 for the selected context.
These measures are applied consistently on both pages, but the overview summarizes at global level while the drillthrough applies them for a single country.

5. How to Use
1.	Open the .pbix file in Power BI Desktop.
2.	Go to the Overview page:
o	Use the Select Year slicer to choose a period.
o	Inspect the treemap, cumulative trend and ranking table to identify high-impact countries.
3.	Right-click a country in the matrix and choose Drillthrough → Country Details:
o	Analyze the timeline of daily cases.
o	Review monthly YoY variation to understand accelerations or improvements.
o	Inspect the yearly comparison and heatmap to identify structural patterns.

6. Files
Typical repository content:
•	Power-BI-COVID-19-Analytics-Dashboard-Cumulative-Daily-Case-Trends.pbix
Main Power BI report file.
•	README.md
Project documentation.
•	dataset/ folder with sample source files
7. Possible Extensions
Ideas for future improvements:
•	Add vaccination, testing, or hospitalization metrics to complement case analysis.
•	Include per-capita indicators (cases per 100k inhabitants) for fairer country comparison.
•	Add forecasting models or basic anomaly detection using Python or R scripts in Power BI.
•	Publish the report to Power BI Service and parameterize it for scheduled refresh.

8. Author
Project developed by Juan Manuel Pérez.
•	LinkedIn: https://www.linkedin.com/in/juan-manuel-p%C3%A9rez-garc%C3%ADa-bigdata/
•	Email: juanmanuelccs19@gmail.com
