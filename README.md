# Top Rated IMDb Movies Analysis: Power BI Dashboard

[![Power BI](https://img.shields.io/badge/Power_BI-View_Live_Dashboard-F2C811?style=flat&logo=powerbi&logoColor=black)](https://app.powerbi.com/groups/me/reports/07333ad0-8c1b-47ec-a2b4-24f4ccfcff29/7aacc7dc9b3ffe2eb8ca?ctid=96e7b82d-bfbf-4ce0-87c2-77981e8ab6b9&experience=power-bi)

![Dashboard screenshot](imdb%20movies%20dadhboard.png)

---

## Project Overview

* Live Dashboard: [View the live Power BI report](https://app.powerbi.com/groups/me/reports/07333ad0-8c1b-47ec-a2b4-24f4ccfcff29/7aacc7dc9b3ffe2eb8ca?ctid=96e7b82d-bfbf-4ce0-87c2-77981e8ab6b9&experience=power-bi)
* Tools and Technologies: Power BI Desktop, Power Query, DAX
* Dataset Scope: the raw file holds the 250 top-rated IMDb films. After cleaning, 199 films released between 1921 and 2026 remain, with IMDb rating (8.0 to 9.3), budget, worldwide box office, genre, runtime, content rating and production company. All money values are in US dollars.
* Files: `ToP_movies_on_imdb_in_2026.pbix` (report), `ToP movies on imdb in 2026 Dataset.csv` (data) and a screenshot of the dashboard.

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

1. **The films returned about 5 times their budget.** The 199 films earned $57.33 billion at the box office on $9.19 billion of budgets, a profit of $48.15 billion and an overall ROI of 524.17%. The typical film (median ROI) returned 387%. Only 27 of the 199 films (14%) earned less than they cost.
2. **Action and Adventure take about 66% of all budget money.** Action has $3.41 billion (37%) and Adventure $2.63 billion (29%), followed by Crime ($1.16 billion), Drama ($1.05 billion) and Biography ($0.63 billion). Horror ($37 million), Mystery ($91 million) and Comedy ($176 million) have the smallest budgets.
3. **The largest profits come from big-budget franchise films.** The six most profitable films are Avengers: Endgame ($2.44 billion profit on a $356 million budget), Spider-Man: No Way Home ($1.72 billion), Avengers: Infinity War ($1.70 billion), Top Gun: Maverick ($1.33 billion), Harry Potter and the Deathly Hallows: Part 2 ($1.22 billion) and The Lord of the Rings: The Return of the King ($1.06 billion).
4. **Almost half the films are rated R.** R has 95 films (48%), G 36 (18%), PG 35 (18%) and PG-13 32 (16%). NC-17 has just 1.
5. **PG-13 and R films have the best typical return.** The median ROI is 466% for PG-13, 406% for R and 391% for PG. G films have a median ROI of only 25%, and the single NC-17 film is at 64%.
6. **Normal-length films (121 to 150 minutes) have the best median ROI.** It is 486% for Normal (79 films), 341% for Short (120 minutes or less, 75 films) and 326% for Long (151 minutes or more, 45 films). Long films have the highest average IMDb rating (8.44), ahead of Normal (8.31) and Short (8.26).
7. **The highest ROI belongs to companies with few films.** Selznick International Pictures leads with 10,018%, followed by Zanuck/Brown Productions (5,074%), Asghar Farhadi Productions (4,485%), Aniplex (3,868%) and Wiedemann & Berg Filmproduktion (3,784%). 72 of the 97 companies made only one film in the data, and Lucasfilm, with 3 films, has an ROI of 2,840%.

---

## Recommendations

1. **Judge films on ROI as well as profit.** Big-budget Action and Adventure films make the largest profits, but they take about two thirds of the capital and 14% of all films still lost money. Check ROI before committing a large budget.
2. **Aim for a normal runtime of about 2 to 2.5 hours.** Films of 121 to 150 minutes have the highest median ROI (486%). Longer films did not show higher returns, although their average rating was slightly higher.
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

The raw dataset has 250 films and 27 columns. The dashboard keeps 199 films and 14 columns. The Power Query steps are:

* Removed films with no budget or no worldwide box office (the raw file has 24 films with no budget and 4 with no box office).
* Removed films whose budgets are not in US dollars, so all money values are on one basis. The 7 largest budgets (Japanese yen, Indian rupee and Korean won figures) were removed by rank, and 11 more films were removed by title: High and Low, Maharaja, Seven Samurai, La haine, The Intouchables, Metropolis, The Hunt, Downfall, Lock, Stock and Two Smoking Barrels, Trainspotting and Monty Python and the Holy Grail.
* Removed Animation films and films with no production company, no content rating or a "Not Rated" rating.
* Kept one value for fields that hold lists: the first genre, the first country and the first production company. Company names that contain an apostrophe (such as Loew's) are read correctly, so those films are no longer dropped by mistake.
* Mapped the old content ratings "Approved" to G and "Passed" to PG.
* Added a `Runtime Category` column: Short (120 minutes or less), Normal (121 to 150) and Long (151 or more).
* Dropped unused columns such as links, images, trailer and description, and set data types.

---

## Data Model and DAX

A single data table (`ToP movies on imdb in 2026 Dataset`) and a `Measures Table` that holds the calculations. A flat table is enough here because every column describes one film, so no relationships are needed.

```dax
Total Budget     = SUM('ToP movies on imdb in 2026 Dataset'[budget])
Total Box Office = SUM('ToP movies on imdb in 2026 Dataset'[grossWorldwide])
Total Profit     = [Total Box Office] - [Total Budget]
ROI              = DIVIDE([Total Profit], [Total Budget], 0)
Movie Count      = COUNTROWS('ToP movies on imdb in 2026 Dataset')
Median ROI       = MEDIANX('ToP movies on imdb in 2026 Dataset', [ROI])
```

---

## Data Notes

* **Only highly rated films are included** (ratings of 8.0 and above) and 51 of the top 250 were removed in cleaning, so the results show what top-rated films earn, not what films in general earn. Flops with low ratings are missing.
* **Money is not adjusted for inflation.** Films from 1921 to 2026 are compared in the dollars of their own time, which favours old films with small budgets (Gone with the Wind, 1939, has an ROI of about 10,000%).
* **ROI only uses the film's budget.** Marketing, distribution and the studio's share of ticket sales are not included.
* **Each film has a single genre, country and production company.** Only the first one listed is kept. The data has 8 genres, and Horror and Mystery have only 3 films each, so their results are not reliable.
* **Animation was removed on purpose.** It is a judgement call made during cleaning, so the results describe live-action films only.
* **Currency was checked for most films, not all.** Budgets that were clearly in another currency were removed. Two films, Ran and Demon Slayer, were kept without a confirmed currency.
* **Small groups.** NC-17 has 1 film, and 72 of 97 production companies have 1 film.
* **Median and overall ROI differ.** G films have an overall ROI of about 546% but a median of 25%. The G group includes 1930s to 1960s classics that were labelled "Approved" and mapped to G, and a few big winners carry the total.
* **Box office for old films looks incomplete.** Many films from before 1970 show a box office that is far below their budget (for example 12 Angry Men and On the Waterfront), while Gone with the Wind shows a very high return. ROI for classic films should be read with care.

---

## How to Open

1. Open `ToP_movies_on_imdb_in_2026.pbix` in Power BI Desktop.
2. If the data does not load, go to Transform data > Data source settings > Change Source and select your local copy of `ToP movies on imdb in 2026 Dataset.csv`.
3. The screenshot shows a static view of the dashboard.

---

## Repository Contents

| File | Description |
|---|---|
| `ToP movies on imdb in 2026 Dataset.csv` | Raw film data (250 films, 27 columns) |
| `ToP_movies_on_imdb_in_2026.pbix` | Power BI report |
| `imdb movies dadhboard.png` | Screenshot of the dashboard |
| `README.md` | Project documentation |
