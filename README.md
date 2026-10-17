
# What Explains ERA? A Statistical Analysis of 2025 MLB Pitching

## Project Overview

This project investigates how different pitching statistics individually and collectively explain variation in Earned Run Average (ERA) among Major League Baseball (MLB) pitchers during the 2025 season.

Using R, the analysis examines relationships between ERA and five pitching statistics:

- **K/9:** Strikeouts per nine innings
- **BB/9:** Walks per nine innings
- **HR/9:** Home runs allowed per nine innings
- **H/9:** Hits allowed per nine innings
- **WHIP:** Walks plus hits per inning pitched

The project progresses from exploratory data analysis and individual correlations to multiple linear regression, model comparison, and regression diagnostics.

The primary objective is to identify which pitching statistics provide the greatest explanatory value and determine whether combining multiple variables produces a more informative statistical model.

## Dataset

Data was obtained from [FanGraphs](https://www.fangraphs.com/) using the `baseballr` package in R.

The dataset includes **127 MLB pitchers** who recorded at least 100 innings pitched during the 2025 season.

Each observation represents one pitcher's season-level statistics. The sample may include both starting pitchers and relief pitchers who met the innings threshold.

## Tools and Methods

**Programming Language:** R

**Packages:**
- `tidyverse`
- `ggplot2`
- `baseballr`
- `car`

**Statistical Techniques:**
- Exploratory data analysis
- Data visualization using ggplot2
- Pearson correlation analysis
- Simple linear regression
- Multiple linear regression
- R-squared and adjusted R-squared comparisons
- Nested-model ANOVA
- Variance Inflation Factors (VIF)
- Regression diagnostics
- Cook's Distance and sensitivity analysis

## 1. Exploratory Analysis

Five pitching statistics were individually examined to investigate their linear relationships with ERA.

| Statistic | Pearson Correlation (r) | R² | Variation Explained |
|-----------|------------------------:|---:|--------------------:|
| K/9 | -0.469 | 0.220 | 22.0% |
| BB/9 | 0.333 | 0.111 | 11.1% |
| HR/9 | 0.655 | 0.429 | 42.9% |
| H/9 | 0.864 | 0.747 | 74.7% |
| WHIP | 0.841 | 0.707 | 70.7% |

**Key Finding:** H/9 demonstrated the strongest individual linear relationship with ERA, explaining approximately 74.7% of the observed variation.

## 2. Investigating H/9 and WHIP

A deeper investigation examined whether WHIP provides additional explanatory value beyond H/9.

The two statistics demonstrated a strong positive correlation (r = 0.879), indicating substantial overlapping information.

A combined regression model using both H/9 and WHIP produced:

- **R²:** 0.7763
- **Adjusted R²:** 0.7727
- **VIF:** 4.383 for both predictors

The combined model explained approximately 77.6% of the observed variation in ERA, improving upon either individual model.

However, the VIF results indicated meaningful multicollinearity, which should be considered when interpreting the individual coefficients.

## 3. Multiple Regression Analysis

A multiple linear regression model was developed using H/9, BB/9, HR/9, and K/9.

The initial four-variable model produced:

- **R²:** 0.8551
- **Adjusted R²:** 0.8504

H/9, BB/9, and HR/9 were statistically significant (p < 0.001).

However, K/9 was not statistically significant (p = 0.796), despite demonstrating a moderate negative correlation with ERA during the initial exploratory analysis.

### Model Comparison

Four nested regression models were compared using adjusted R² and ANOVA.

| Model | Predictors | Adjusted R² |
|-------|------------|------------:|
| Model 1 | H/9 | 0.7452 |
| Model 2 | H/9 + BB/9 | — |
| Model 3 | H/9 + BB/9 + HR/9 | **0.8515** |
| Model 4 | H/9 + BB/9 + HR/9 + K/9 | 0.8504 |

The ANOVA comparisons demonstrated that adding BB/9 and HR/9 significantly improved model fit (p < 0.001), while adding K/9 did not (p = 0.796).

**Model 3 was selected as the preferred model**, achieving slightly higher adjusted explanatory power with fewer predictors.

### Multicollinearity

Variance Inflation Factors for Model 3 were:

| Predictor | VIF |
|-----------|----:|
| H/9 | 1.339 |
| BB/9 | 1.039 |
| HR/9 | 1.295 |

All VIF values were below 1.34, suggesting that multicollinearity was not a major concern.

### Regression Diagnostics

Residual diagnostic plots were examined to evaluate model assumptions.

The analysis identified:

- No major nonlinear patterns in the residuals
- Some departures from normality in the tails
- Possible mild heteroscedasticity
- Several potentially influential observations

These findings suggest that the preferred model provides a reasonable linear representation of the dataset, while some limitations remain.

### Influential Observations

Cook's Distance was used to identify potentially influential observations.

Eight pitchers exceeded the screening threshold of 4/n.

A sensitivity analysis was conducted by excluding these observations and refitting Model 3 using the remaining 119 pitchers.

The sensitivity model produced an adjusted R² of 0.8704, compared with 0.8515 for the original model.

The estimated coefficients for H/9 and HR/9 changed by approximately 1.8% and 5.1%, respectively. However, BB/9 increased by approximately 38.2%, indicating greater sensitivity to influential observations.

The original model was retained as the primary analysis.

## 4. Key Findings

The analysis produced several important findings:

1. **H/9 was the strongest individual predictor of ERA**, explaining approximately 74.7% of the observed variation.

2. **Combining multiple statistics improved explanatory power.** The preferred three-variable model achieved an adjusted R² of approximately 0.8515.

3. **K/9 provided little additional explanatory value** after accounting for H/9, BB/9, and HR/9, despite its moderate individual relationship with ERA.

4. **Model complexity did not necessarily improve performance.** Removing K/9 slightly increased adjusted R² while simplifying the model.

5. **Influential observations affected some coefficient estimates**, particularly BB/9, highlighting the importance of diagnostic testing and sensitivity analysis.

## 5. Limitations

- The analysis examines only the 2025 MLB season.
- Only pitchers with at least 100 innings pitched were included.
- ERA is influenced by defense, ballpark conditions, opponent quality, and sequencing.
- Hits, walks, and home runs are directly related to run-scoring events, creating inherent relationships with ERA.
- Some deviations from regression assumptions were observed.
- The model's explanatory power was evaluated within the sample and should not be interpreted as future predictive accuracy.
- Statistical relationships do not establish causation.

## 6. Future Research

Potential extensions include:

- Examining multiple MLB seasons to evaluate the consistency of the results.
- Investigating alternative measures such as ERA+ and Fielding Independent Pitching (FIP).
- Incorporating advanced pitching metrics, including hard-hit rate and ground-ball rate.
- Developing models that use previous-season statistics to predict future ERA.
- Evaluating predictive performance using separate training and testing datasets.

## Data Source

[FanGraphs](https://www.fangraphs.com/)

Data retrieved using the `baseballr` package in R.

## Author

**Borna Anic-Matic**

Independent baseball analytics project developed using R and R Markdown.
