# 🔢 Module 07: Describing Data

## Completed Module Commentary
This module explained...
- Types of data (what a column means vs. how it's stored)
- The "center" and "spread" of data
- Determining the shape of data and identifying outliers
- Comparing data groups
- Describing relationships and correlation between groups

- One thing that clicked for me in this module was interpreting what data is actually "saying". One thing that may be worth revisiting is the overall pipeline for inspecting, cleaning, and comparing data. The content in this module was clear and well-organized, with no glaring issues that I would change.

---

## 🔗 Completed Assignments

| Notebook | Description |
|----------|-------------|
| [01-Types_of_Data.ipynb](01-Types_of_Data.ipynb) | This notebook explained, **dtype vs. meaning**: the difference between qualitative and quantitative variables, discrete/continuous, the four scales (nominal, ordinal, interval, ratio), etc. |
| [02-Center_and_Spread.ipynb](02-Center_and_Spread.ipynb) | This notebook explained `.mean()`/`.median()`/`.mode()` and robustness, how `ddof` affects results for pandas and NumPy, percentiles and the IQR, and more. |
| [03-Shape_and_Outliers.ipynb](03-Shape_and_Outliers.ipynb) | This notebook explored the difference between Symmetric and skewed data, the use of `.skew()` and `.kurt()`, IQR fence rules, z-scores, the importance of inspecting, etc. |
| [04-Comparing_Groups.ipynb](04-Comparing_Groups.ipynb) | This notebook explored group summaries with size + center + spread, the difference between rates and counts, how `pd.crosstab()` is used with `normalize=`, `pivot_table()`, **confounders**, etc. |
| [05-Relationships_and_Correlation.ipynb](05-Relationships_and_Correlation.ipynb) | This notebook covered Covariance vs. correlation, the use of `.corr()` for a pair or a matrix, how to list the strongest pairs, **Pearson vs. Spearman**, **Anscombe's quartet**, and more. |
| [06-Describing_Data_Lab.ipynb](06-Describing_Data_Lab.ipynb) | This notebook was a lab that walked through the process of describing the Palmer Penguins dataset from raw file to saved report. |