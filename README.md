# What Makes a Music Artist Successful?

Group project for **Programming for Data Science 2026/2027**, NOVA IMS, Bachelor's in Data Science, **Group [05]**.

This project analyses the all-time streaming data of 500 of the world's most-streamed music artists to understand which factors are associated with their success. It covers data cleaning and analysis, web scraping of each artist's birthplace from Wikipedia, interactive world maps of streams, and [one sentence on the 4.3 idea].

## Group members

| Name | Student number |
|---|---|
| José Jesus | 20251389 |
| Lara Barradas | 20251397 |
| Lara Manso | 20251364 |
| Zahra Ahamed | 20251382 |

## Project structure

The work was divided into parts, each developed in its own notebook and later merged into the final notebook.

| Part | Notebook | Content | Author |
|---|---|---|---|
| 2.1–2.3 Data wrangling | `[A's notebook].ipynb` | Data quality and cleaning (Q1), basic exploratory analysis (Q2), data update analysis (Q3) | [name] |
| 2.4–2.5 Analysis | `B_analysis.ipynb` | Career length and collaborations (Q4), additional insights (Q5) | [name] |
| 3.1 Web scraping | `Web_Scraping_PDS_project.ipynb` | Birthplace or origin of each artist and its coordinates, scraped from Wikipedia starting from the Main Page | José Jesus |
| 3.2 Interactive maps | `[D's notebook].ipynb` | World map with one marker per artist (sized by total streams) and density map of streams by birthplace | [name] |
| 4. Data Science in Action | `[notebook].ipynb` | [short description of the 4.3 idea] | [names] |
| Final notebook | `GroupXX_PDS_2627.ipynb` | All parts merged, run from start to finish | All |

## Data flow

```
artist_streams.csv                       original dataset (provided by the course)
        │
        ▼  2.1 Data cleaning
artist_streams_cleaned.csv               one row per artist, cleaned
        │
        ├──▶ 2.2–2.5 Analysis (Q2–Q5)
        │
        ▼  3.1 Web scraping (Wikipedia)
artist_streams_with_locations.csv        cleaned data + birthplace and coordinates
        │
        ▼
3.2 Interactive maps  ──▶  4. Data Science in Action
```

## Datasets

| File | Description |
|---|---|
| `artist_streams.csv` | Original dataset: 511 rows, including 10 duplicates and 1 empty row |
| `artist_streams_cleaned.csv` | Cleaned dataset: 500 artists, one row each |
| `artist_streams_with_locations.csv` | Cleaned dataset with the scraped columns below |
| `scrape_progress.csv` | Saved results of the scraping, so the notebook can be rerun without scraping Wikipedia again |

Columns added by the web scraping:

| Column | Meaning |
|---|---|
| `Birthplace` | Birthplace (solo artists) or origin (groups), as written in the Wikipedia infobox |
| `Latitude`, `Longitude` | Coordinates of that place, in decimal degrees |
| `Wikipedia Page` | Article used for the artist |
| `Coordinates From` | Page that provided the coordinates |
| `Match Quality` | `strong` (page name equals the artist's name) or `weak` (one name contains the other) |
| `Scrape Status` | `ok`, `no_article`, `no_birthplace` or `no_coordinates` |

## How to run

1. Clone the repository, or download it as a ZIP (green **Code** button → **Download ZIP**).
2. Install the packages:

   ```
   pip install pandas numpy matplotlib seaborn plotly requests beautifulsoup4 selenium
   ```

3. Open `GroupXX_PDS_2627.ipynb` and run all cells from top to bottom (**Restart & Run All**). All CSV files must be in the same folder as the notebook.

Notes:
- The web scraping section needs an internet connection. Because `scrape_progress.csv` is included, it does not scrape Wikipedia again: it only reads the saved results. Without that file, scraping all 500 artists takes about one hour.
- One cell uses Selenium to open the Wikipedia Main Page in Google Chrome, so Chrome must be installed. If it is not, the cell prints a message and the rest of the notebook still runs.
- The scraping was run on 10 November 2026. Wikipedia pages change over time, so a new run may give slightly different results.

## Package versions

| Package | Version |
|---|---|
| Python | 3.13.15 |
| pandas | 3.0.6 |
| numpy | [version] |
| matplotlib | [version] |
| seaborn | [version] |
| plotly | [version] |
| requests | 2.34.2 |
| beautifulsoup4 | 4.15.0 |
| selenium | 4.47.0 |

The notebook also prints the version of every package it uses.

## Main results

- **Data quality:** 10 duplicated rows and 1 empty row were removed, leaving 500 artists. Missing stream values were filled using the relationships between the stream columns.
- **The dataset:** 102 pop artists; Hip-Hop is the most common genre (115 artists), the United States the most common country (265 artists), and English, Spanish and Portuguese the most common languages.
- **Updates:** the most recent update was on 1 July 2026 and the oldest on 1 July 2025. 10 artists have stream counts last updated before the end of 2025.
- **Career length and collaborations:** [main conclusions of Q4].
- **Additional insights:** [the three insights of Q5].
- **Web scraping:** the birthplace or origin and its coordinates were obtained for 454 of the 500 artists (90.8%). Weak matches and differences from the dataset's country were reviewed by hand.
- **Interactive maps:** [main conclusions of the maps].
- **Data Science in Action:** [main conclusion of 4.3].

## Data sources

- **Artist streaming data:** provided by the course (`artist_streams.csv`).
- **Birthplaces and coordinates:** [Wikipedia](https://en.wikipedia.org/wiki/Main_Page), scraped with `requests` and `BeautifulSoup`, starting from the Main Page. The scraper identifies itself with a User-Agent and pauses between requests, following Wikipedia's usage guidelines.

## Workflow

Each part was developed on its own branch and merged into `main` through a pull request, reviewed by another group member, so `main` always contains working versions.
