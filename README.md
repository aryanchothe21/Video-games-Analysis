# Video Game Sales: Exploratory Data Analysis

Exploratory analysis of global video game sales (16,598 titles, 1980–2020) using Python. The notebook cleans and explores the data, then looks at genre, platform, publisher, region and release-year patterns with pandas, matplotlib and seaborn.

**Notebook:** [`Videogames_analysis.ipynb`](Videogames_analysis.ipynb)
**Author:** Aryan · [github.com/aryanchothe21](https://github.com/aryanchothe21)

---

## Dataset

| Item | Detail |
|---|---|
| Source | [Video game sales dataset on Zenodo](https://zenodo.org/records/5898311/files/vgsales.csv) (loaded directly in the notebook, no download needed) |
| Size | 16,598 rows × 11 columns |
| Period | 1980 – 2020 |
| Sales unit | Millions of copies |

**Columns:** `Rank`, `Name`, `Platform`, `Year`, `Genre`, `Publisher`, `NA_Sales`, `EU_Sales`, `JP_Sales`, `Other_Sales`, `Global_Sales`

**Data quality notes**
- `Year` has 271 missing values (16,327 of 16,598 present).
- 11,493 unique game names across 16,598 rows, because one game can appear once per platform.

---

## What I did

1. **Loaded and inspected** the data (`head`, `describe`, unique values).
2. **Genre analysis:** counted games per genre (bar chart, count plot).
3. **Regional analysis:** summed NA, EU, JP and Other sales and compared them (pie chart).
4. **Distribution analysis:** histogram, KDE and boxplot of release years and global sales.
5. **Trend analysis:** global sales per release year (line plot); case study of *Need for Speed: Most Wanted* compared with the overall trend.
6. **Relationships:** scatter plots (Year vs sales, Rank vs NA sales).
7. **Publisher and platform analysis:** counted titles per publisher and platform.
8. **Focused subset:** filtered to the top 3 publishers × top 3 platforms × top 3 genres (617 titles) and compared them with count plots, boxplots, a correlation heatmap and a pair plot.

---

## Key insights

**1. North America dominates sales.**
NA accounts for about 4,393M of roughly 8,916M units in total (~49%), followed by Europe (~27%), Japan (~14%) and the rest of the world (~9%).

| Region | Sales (M) | Share |
|---|---|---|
| North America | 4,392.95 | 49.3% |
| Europe | 2,434.13 | 27.3% |
| Japan | 1,291.02 | 14.5% |
| Other | 797.75 | 8.9% |

**2. Sales are extremely skewed: a few blockbusters, many small sellers.**
The average title sold 0.54M copies, but the median is only 0.17M, and 75% of titles sold under 0.47M. The top seller, *Wii Sports*, sold 82.74M. The boxplot of `Global_Sales` shows a long tail of outliers.

**3. Nintendo owns the top of the chart.**
The top 5 titles are all Nintendo: Wii Sports, Super Mario Bros., Mario Kart Wii, Wii Sports Resort and Pokemon Red/Blue.

**4. Action and Sports lead by number of releases.**
Action has 3,316 titles and Sports 2,346, while Puzzle has the fewest (582). Release count is not the same as revenue, so a high count does not mean the genre earns the most.

**5. The Japanese market behaves differently.**
The median `JP_Sales` is 0.00, meaning more than half of all titles recorded effectively no sales in Japan, versus a median of 0.08M in North America. Many Western releases never reach Japan, while some Japan-focused titles sell almost only there.

**6. Many games are multi-platform releases.**
About 31% of rows are extra platform versions of a game already in the data. *Need for Speed: Most Wanted* appears 12 times, the most of any title.

**7. DS and PS2 have the most titles.**
DS (2,163) and PS2 (2,161) are nearly tied, ahead of PS3 (1,329), Wii (1,325) and X360 (1,265).

**8. The publisher market has a long tail.**
578 publishers appear in the data. Electronic Arts (1,351), Activision (975), Namco Bandai (932), Ubisoft (921) and Konami (832) lead by count, while many publishers have only a single title.

**9. Releases cluster around the mid-2000s.**
The median release year is 2007 (range 1980–2020), which matches the DS / PS2 / Wii / X360 era.

---

## Hidden patterns and caveats

- **`Rank` is derived from `Global_Sales`.** The dataset is sorted by sales, so a strong negative correlation between them is built in and is not a real finding. The same applies to `Global_Sales` versus the regional columns, since it is their sum.
- **Mean vs median:** because of the skew, the median describes a "typical" game better than the mean.
- **Counts vs sales:** the most-released genre, platform and publisher are not necessarily the most profitable ones. Comparing total and average sales per group gives a different picture.
- **Missing years:** the 271 titles without a `Year` are left out of year-based charts.
- **Recent years are thin:** the last few years in the data have far fewer records, so the tail of the yearly trend line should not be read as a real market decline.

---

## Tools and libraries

- Python 3
- pandas, NumPy
- matplotlib, seaborn
- Google Colab / Jupyter Notebook

Install locally:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

## How to run

```bash
git clone https://github.com/aryanchothe21/<repo-name>.git
cd <repo-name>
jupyter notebook Videogames_analysis.ipynb
```

Or upload the notebook to [Google Colab](https://colab.research.google.com) and choose **Runtime → Run all**. An internet connection is needed because the dataset is read from a URL.

---

## Possible next steps

- Total and average sales per genre, platform and publisher
- Genre preferences by region (for example, role-playing games in Japan vs North America)
- Share of sales from the top 1% / top 10% of titles
- Peak sales year per platform and platform lifecycle curves
- Predicting global sales from genre, platform and publisher
