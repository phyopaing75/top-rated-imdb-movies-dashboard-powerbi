# Top Rated IMDb Movies Analysis: Power BI Dashboard

[![Power BI](https://img.shields.io/badge/Power_BI-View_Live_Dashboard-F2C811?style=flat&logo=powerbi&logoColor=black)](https://app.powerbi.com/groups/me/reports/a52f423e-1f12-4c99-82f5-5fe6311b1687/7aacc7dc9b3ffe2eb8ca?ctid=96e7b82d-bfbf-4ce0-87c2-77981e8ab6b9&experience=power-bi)

---

## Project Overview

* Live Dashboard: [View the live Power BI report](https://app.powerbi.com/groups/me/reports/a52f423e-1f12-4c99-82f5-5fe6311b1687/7aacc7dc9b3ffe2eb8ca?ctid=96e7b82d-bfbf-4ce0-87c2-77981e8ab6b9&experience=power-bi)
* Tools and Technologies: Power BI Desktop, Power Query, DAX
* Dataset Scope: the raw file holds the 250 top-rated IMDb films. After cleaning, 200 films released between 1921 and 2026 remain, with IMDb rating (8.0 to 9.3), budget, worldwide box office, genre, runtime, content rating and production company.
* Files: `ToP_movies_on_imdb_in_2026.pbix` (report), `ToP movies on imdb in 2026 Dataset.csv` (data) and a PDF export of the dashboard.

---

## Business Problem

Film producers and investors want to know where money has been made on well-reviewed films. Total box office is easy to see, but it hides how much each film cost to make. This project compares budget, box office, profit and return on investment (ROI) across genres, content ratings, runtime categories and production companies for top-rated films, using a single Power BI dashboard.

---

## Business Questions

| # | Business question | Dashboard visual |
|---|---|---|
| 1 | How much did the films cost, earn and return overall? | KPI cards: Movie Count, Total Box Office, Total Budget, Total Profit, ROI % |
| 2 | Which genres receive the biggest budgets? | Budgets by Genres (bar chart) |
| 3 | How does box office relate to budget, and which films make the biggest profit? | Box Office by Budgets (scatter plot, bubble size is profit) |
| 4 | Which content ratings are most common, and which give the best return? | Number of Movies per Content Rating (donut); Median ROI by content rating (line chart) |
| 5 | Does runtime affect return and rating? | Median ROI and Average Rating by Runtime Category (combo chart) |
| 6 | Which production companies give the best return? | ROI per Production Company (table) |

---

## Key Insights

All figures come from the dashboard visuals. ROI is profit divided by budget, shown as a percentage.

1. **The films returned about 5 times their budget.** The 200 films earned $53.91 billion at the box office on $8.60 billion of budgets, a profit of $45.31 billion and an overall ROI of 527.01%.
2. **Action and Adventure take about 63% of all budget money.** Action has $3.21 billion (37%) and Adventure $2.20 billion (26%), followed by Crime ($1.17 billion), Drama ($1.07 billion) and Biography ($0.63 billion). Horror ($37 million), Mystery ($91 million) and Comedy ($184 million) have the smallest budgets.
3. **The largest profits come from big-budget franchise films.** The six most profitable films are Avengers: Endgame ($2.44 billion profit on a $356 million budget), Avengers: Infinity War ($1.70 billion), Top Gun: Maverick ($1.33 billion), Harry Potter and the Deathly Hallows: Part 2 ($1.22 billion), The Lord of the Rings: The Return of the King ($1.06 billion) and Jurassic Park ($1.04 billion). All six are Action or Adventure. Even so, 28 of the 200 films earned less at the box office than they cost to make.
4. **Half the films are rated R.** R has 99 films (49.5%), PG 36 (18%), G 34 (17%) and PG-13 30 (15%). NC-17 has just 1.
5. **PG-13 and R films have the best typical return.** The median ROI is 466% for PG-13, 408% for R and 380% for PG. G films have a median ROI of only 8%, and the single NC-17 film is at 64%.
6. **Normal-length films (121 to 150 minutes) have the best median ROI.** It is 485% for Normal, 341% for Short (120 minutes or less) and 334% for Long (151 minutes or more). Long films have the highest average IMDb rating (8.44), ahead of Normal (8.31) and Short (8.25).
7. **The highest ROI belongs to companies with few films.** Selznick International Pictures leads with 10,018%, followed by Zanuck/Brown Productions (5,074%), Asghar Farhadi Productions (4,485%), Quad (4,390%) and Aniplex (3,868%). 75 of the 100 companies made only one film in the data, and Lucasfilm, with 3 films, has an ROI of 2,840%.

---

## Recommendations

1. **Judge films on ROI as well as profit.** Big-budget Action and Adventure films make the largest profits, but they take most of the capital and 14% of the films still lost money. Check ROI before committing a large budget.
2. **Aim for a normal runtime of about 2 to 2.5 hours.** Films of 121 to 150 minutes have the highest median ROI (485%). Longer films did not show higher returns, although their average rating was slightly higher.
3. **Look at the track record of companies with several films.** The top ROI list is led by one-film companies and old classics, so a company with several successful films, such as Lucasfilm (2,840% over 3 films), is a stronger signal than a single hit.

---

## Dashboard Design

| Visual | Type | Fields |
|---|---|---|
| Movie Count, Total Box Office, Total Budget, Total Profit, ROI % | Cards | Measures |
| Budgets by Genres | Bar chart | Sum of `budget` by `genres` |
| Box Office by Budgets | Scatter plot | X: sum of `budget`; Y: sum of `grossWorldwide`; one point per film; colour by genre; size by Total Profit |
| Number of Movies per Content Rating | Donut chart | Count of films by `contentRating` |
| Median ROI by content rating | Line chart | Median ROI by `contentRating` |
| Median ROI and Average Rating by Runtime Category | Combo chart | Runtime Category with an ROI series and an IMDb rating series |
| ROI per Production Company | Table | `productionCompanies` with ROI % |
| Movie Titles | Slicer | `primaryTitle` |

---

## Data Cleaning

The raw dataset has 250 films. The dashboard keeps 200 of them. Films were removed when:

* the budget was not in US dollars, so it could not be compared with the other budgets, or
* a budget or box office value was missing (the raw file has 24 films with no budget and 4 with no worldwide box office).

Removing these 50 films keeps every budget, box office, profit and ROI figure on one consistent dollar basis.

---

## Data Model and DAX

A single data table (`ToP 250 movies on imdb in 2026`) and a `Measures Table` that holds the calculations. The runtime categories are Short (68 to 120 minutes), Normal (121 to 150) and Long (151 to 238).

```dax
Total Budget     = SUM('ToP 250 movies on imdb in 2026'[budget])
Total Box Office = SUM('ToP 250 movies on imdb in 2026'[grossWorldwide])
Total Profit     = [Total Box Office] - [Total Budget]
ROI              = DIVIDE([Total Profit], [Total Budget], 0)
Movie Count      = COUNTROWS('ToP 250 movies on imdb in 2026')
Median ROI       = MEDIANX('ToP 250 movies on imdb in 2026', [ROI])
```

---

## Data Notes

* **Only highly rated films are included** (ratings of 8.0 and above) and 50 of the top 250 were removed in cleaning, so the results show what top-rated films earn, not what films in general earn. Flops with low ratings are missing.
* **Money is not adjusted for inflation.** Films from 1921 to 2026 are compared in the dollars of their own time, which favours old films with small budgets (Gone with the Wind, 1939, has an ROI of about 10,000%).
* **ROI only uses the film's budget.** Marketing, distribution and the studio's share of ticket sales are not included.
* **Each film has a single main genre.** The data has 8 genres, and Horror and Mystery have only 3 films each, so their results are not reliable.
* **The table name still says "Top 250".** It holds the 200 films that remained after cleaning (see Data Cleaning). Renaming the table to match would avoid confusion.
* **Small groups.** NC-17 has 1 film, and 75 of 100 production companies have 1 film.
* **Median and overall ROI differ.** G films have an overall ROI of about 579% but a median of 8%, because a few blockbusters carry the total. The overall ROI for all films is 527% and the median film ROI is 384%.
* **The runtime rating line plots the sum of IMDb ratings, not the average.** Each category's sum depends on how many films it holds (648.3 for Normal, 635.5 for Short, 379.7 for Long). Change that field to Average of `averageRating` so the chart matches its title. The averages are calculated correctly.

---

## How to Open

1. Open `ToP_movies_on_imdb_in_2026.pbix` in Power BI Desktop.
2. If the data does not load, go to Transform data > Data source settings > Change Source and select your local copy of `ToP movies on imdb in 2026 Dataset.csv`.
3. The PDF shows a static view of the dashboard.

---

## Repository Contents

| File | Description |
|---|---|
| `ToP movies on imdb in 2026 Dataset.csv` | Raw film data (250 films, 27 columns) |
| `ToP_movies_on_imdb_in_2026.pbix` | Power BI report |
| `Top Rated IMDB Movies Analysis.pdf` | PDF export of the dashboard |
| `README.md` | Project documentation |
