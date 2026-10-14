
# What Explains ERA? A Statistical Analysis of 2025 MLB Pitching

## Project Overview

This project examines the relationship between several pitching statistics and Earned Run Average (ERA) among Major League Baseball (MLB) pitchers during the 2025 season.

The goal is to determine how well different pitching statistics explain variation in ERA and identify which statistics have the strongest individual linear relationships with pitching performance.

The analysis focuses on five statistics:

- **K/9:** Strikeouts per nine innings
- **BB/9:** Walks per nine innings
- **HR/9:** Home runs per nine innings
- **H/9:** Hits allowed per nine innings
- **WHIP:** Walks plus hits per inning pitched

## Dataset

The dataset was obtained from [FanGraphs](https://www.fangraphs.com/) using the `baseballr` package in R.

The analysis includes MLB pitchers who recorded at least **100 innings pitched during the 2025 season**.

Each observation represents one pitcher's season-level statistics.

## Tools and Methods

**Programming Language:** R

**Packages Used:**
- `tidyverse`
- `ggplot2`
- `baseballr`
- `car`

**Statistical Methods:**
- Exploratory data analysis
- Scatterplots with linear regression trend lines
- Pearson correlation coefficients
- Coefficients of determination (R²)
- Comparison of individual predictors

## Results

The following table summarizes the relationships between each pitching statistic and ERA.

| Statistic | Pearson Correlation (r) | R² | Variation Explained |
|-----------|------------------------:|---:|--------------------:|
| K/9       | -0.469 | 0.220 | 22.0% |
| BB/9      | 0.333  | 0.111 | 11.1% |
| HR/9      | 0.655  | 0.429 | 42.9% |
| H/9       | 0.864  | 0.747 | 74.7% |
| WHIP      | 0.841  | 0.707 | 70.7% |

## Key Findings

**H/9 demonstrated the strongest individual linear relationship with ERA**, explaining approximately 74.7% of the variation among pitchers in the dataset.

WHIP followed closely at 70.7%. Despite incorporating both hits and walks, WHIP had a slightly weaker individual relationship with ERA than H/9.

HR/9 explained approximately 42.9% of the variation, while K/9 and BB/9 demonstrated weaker relationships.

These findings suggest that statistics measuring hits and baserunners allowed have particularly strong associations with ERA.

However, correlation does not establish causation, and these results do not necessarily indicate which statistics are the most important causes of pitching performance.

## Limitations

- The analysis only includes pitchers with at least 100 innings pitched.
- Only the 2025 MLB season was examined.
- Each pitching statistic was analyzed individually.
- The analysis does not yet account for relationships between multiple predictors.
- ERA may also be influenced by defensive performance, ballpark conditions, and the sequencing of hits and walks.

## Future Development

Future work will focus on:

- Multiple linear regression to examine the collective explanatory power of pitching statistics.
- Multicollinearity testing to identify overlapping predictors.
- Model diagnostics and additional statistical testing.
- Potential comparisons across multiple MLB seasons.

## Data Source

**FanGraphs:** https://www.fangraphs.com/

Data retrieved using the `baseballr` package in R.

## Author

**Borna Anic-Matic**

Independent baseball analytics project developed using R and R Markdown.
