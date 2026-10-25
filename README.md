# Customer Spending Analysis

Analysis of 2,000 retail customers: do demographics or income predict spending? Python, statistical testing and clustering.

---

## Project Overview

A retailer wants to increase customer spending and needs to know where to focus its marketing. This project examines a dataset of 2,000 customers to answer three questions:

1. Who are the retailer's customers?
2. What drives how much they spend?
3. Are there distinct customer segments worth targeting?

## Summary of Findings

- **Demographics do not explain spending.** There was no statistically significant difference in spending score by gender (p = 0.70), age group (p = 0.19) or profession (p = 0.59).
- **Income does not explain spending either.** The correlation between income and spending score was 0.02 (p = 0.31), and average spending scores were similar across all five income bands (roughly 49 to 53).
- **No natural customer segments were found.** Silhouette scores were similar for every number of clusters tested (about 0.35 to 0.38), so any clustering would be arbitrary rather than meaningful.
- **One weak lead:** customers under 18 scored about 4 points higher than adults (p = 0.029). This was an exploratory comparison made after viewing the averages, so I treat it as a possible lead rather than a firm conclusion.

**Conclusion:** the demographic and income data available cannot identify which customers to target. The retailer would need behavioural data, such as purchase history and visit frequency, to answer this question.

## Data

- **Source:** https://www.kaggle.com/datasets/datascientistanna/customers-dataset?resource=download
- **Size:** 2,000 customers, 8 columns (1,972 rows after cleaning)
- **Columns:** Customer ID, Gender, Age, Annual Income ($), Spending Score (1-100), Profession, Work Experience, Family Size

Please note that the data is very evenly distributed, which suggests it may be synthetic. Findings may differ with real transaction data.

## Method

1. **Cleaning:** reviewed duplicates, missing values and implausible entries (see the cleaning log below).
2. **Exploration:** summary statistics and averages by gender, age group and profession.
3. **Hypothesis testing:** Welch's t-test for gender, one-way ANOVA for age group and profession, and an exploratory t-test for under-18s versus adults.
4. **Correlation analysis:** correlation matrix and Pearson test for income against spending score, plus spending by income band.
5. **Clustering:** K-means on income and spending score, evaluated with silhouette scores for 2 to 8 clusters.

### Data Cleaning Log

| Issue | Rows affected | Action |
|---|---|---|
| Duplicate records | 0 | None needed |
| Missing profession | 35 | Kept and labelled "Unknown", as the other fields were still usable |
| Age recorded as 0 | 24 | Removed as invalid |
| Annual income of 0 | 2 | Removed as likely errors |
| Spending score of 0 | 2 | Removed as likely errors |
| Lowest incomes ($1,000 to $4,000) | 10 | Reviewed and kept as plausible |
| Work experience inconsistent with age | Roughly one in five rows | Retained, but treated with caution and not relied on in the analysis |

**Final dataset: 1,972 rows.** Removing the zero-value rows changed the mean income and mean spending score by less than 0.5%.

## Key Visualisations

### Average Spending Score by Profession


### Average Spending Score by Income Band


### Correlation Between Customer Variables



## Recommendations

1. **Do not target customers by demographics or income.** Campaigns aimed at a particular gender, age band, profession or income level are unlikely to reach high spenders more effectively than broad campaigns.
2. **Collect behavioural data.** Purchase history, product categories, visit frequency, basket size and loyalty card activity are more likely to predict spending than the variables available here.
3. **Repeat the segmentation once that data is available.** The method in this notebook can be reused directly.
4. **Test the under-18 lead with a small pilot.** A low-cost trial offer would show whether the difference is genuine before any strategy is built on it.
5. **Clarify how the spending score is calculated.** If it is a store-assigned rating rather than a record of actual purchases, that may explain why no variable predicts it.

## Limitations

- The data is a single snapshot and contains no transaction-level detail.
- The analysis identifies associations only and cannot establish causation.
- The data appears to be synthetic, so real-world results may differ.
- Work experience values were inconsistent with age for many records.
- Several tests were run, which increases the chance of a false positive. The under-18 result should be read with this in mind.

## How to Run

1. Open `notebook/customer_analysis.ipynb` in [Google Colab](https://colab.research.google.com).
2. Upload `data/Customers.csv` to the Colab file panel.
3. Select **Runtime > Run all**.

## Tools Used

Python, pandas, NumPy, matplotlib, seaborn, SciPy, scikit-learn, Google Colab


## About the Author

I am Echie Ugbekile, a BSc Mathematics student at Coventry University, based in London, with a focus on data analysis. I hold the IBM Data Analyst Professional Certificate and work with Excel, Python and SQL. This project reflects my approach to analysis: begin with a clear business question, document every decision, and report findings honestly, including when the data does not support a convenient conclusion.

**Contact:**
Email: Echie.ugbekile@gmail.com
