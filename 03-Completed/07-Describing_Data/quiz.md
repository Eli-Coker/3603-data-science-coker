# 📝 Quiz: 07 - Describing Data

36 questions covering types of data, center and spread, shape and outliers, comparing groups, and relationships and correlation. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Types of Data

**1.** (Short Answer) What's the difference between a column's **dtype** and its **measurement scale**?

**Answer:** A column's **dtype** is how pandas stores the values, while its **measurement scale** is what the values mean.

**2.** (Multiple Choice) Titanic's `Pclass` is stored as `1`, `2`, `3`. Its measurement scale is:
A) Nominal  B) Ordinal  C) Interval  D) Ratio 

**Answer:** B) Ordinal

**3.** (Multiple Choice) Which scale has a true zero that means "none of it"?
A) Nominal  B) Ordinal  C) Interval  D) Ratio

**Answer:** D) Ratio

**4.** (True/False) Temperature in °C is ratio data, because 20°C is twice 10°C.

**Answer:** False

**5.** (Short Answer) Is "number of siblings aboard" discrete or continuous? How can you tell?

**Answer:** "Number of siblings aboard" is **discrete**, as it is countable with gaps between possible values.

**6.** (Code Tracing) What prints?
```python
s = pd.Series([True, False, True, True])
print(s.mean())
```
**Answer:** 0.75

**7.** (Short Answer) Why is `titanic['PassengerId'].mean()` meaningless, even though pandas computes it without complaint?

**Answer:** `'PassengerId'` is an identifier label, not a measurement, thus computing the .mean gives meaningless output.

**8.** (Short Answer) What does `ordered=True` in `pd.CategoricalDtype([...], ordered=True)` let you do that a plain `str` column can't?

**Answer:** `ordered=True` tells pandas the *meaningful order* for provided categories.
---

## Section B — Center and Spread

**9.** (Short Answer) Which is more robust to outliers, the mean or the median? Why?

**Answer:** The *median* is more robust to outliers as it depends only on the middle position.

**10.** (Code Tracing) What prints?
```python
s = pd.Series([2, 4, 4, 6, 100])
print(s.median(), s.mode()[0])
```
**Answer:** 4.0 4

**11.** (Short Answer) A column's mean is much larger than its median. What does that suggest?

**Answer:** A column's mean being larger than the median suggests that it is **right-skewed (positive)**.

**12.** (Multiple Choice) `pd.Series(data).std()` and `np.std(data)` give slightly different answers because:
A) NumPy rounds  B) pandas skips NaN  C) they use different default `ddof`  D) one is variance

**Answer:** C) they use different default `ddof`

**13.** (Short Answer) What's the IQR, and how do you compute it in pandas?

**Answer:** The *IQR* is the width of the middle half of the data. To compute it in pandas, perform `s.quantile(0.75) - s.quantile(0.25)`.

**14.** (Short Answer) In `.describe()`, a column's `count` is 714 but the DataFrame has 891 rows. What does that tell you?

**Answer:** This tells you that the column contains *missing values*.

**15.** (Short Answer) You fill 177 missing ages with the median age. What happens to the standard deviation, and why?

**Answer:** The standard deviation (std) shrinks because you added 177 identical values right at the center, thus making the data appear less spread out than it really is.

**16.** (Short Answer) Which spread statistic pairs naturally with the median, and which with the mean?

**Answer:** The *IQR* pairs naturally with the median, and the *std* with the mean.

---

## Section C — Shape and Outliers

**17.** (Multiple Choice) A column with `.skew()` of 4.8 is:
A) roughly symmetric  B) strongly left-skewed  C) strongly right-skewed  D) heavy-tailed but symmetric

**Answer:** C) strongly right-skewed

**18.** (Short Answer) Write the formulas for the lower and upper fences of the 1.5 × IQR rule.

**Answer:** lower fence = Q1 − 1.5 × IQR | upper fence = Q3 + 1.5 × IQR

**19.** (Short Answer) On Titanic fares, the IQR rule flags 116 values but the |z| > 3 rule flags only 20. Why are z-scores less sensitive on a skewed column?

**Answer:** Since Z-scores are built from the mean and std, they are less sensitive on a skewed column as both mean and std are inflated.

**20.** (True/False) Any value flagged as an outlier should be removed before analysis.

**Answer:** False

**21.** (Short Answer) Name two things you can do with a real-but-extreme value instead of deleting it.

**Answer:** Instead of deleting a real-but-extreme value, you can keep it and *use robust statistics*, or *report it separately*.

**22.** (Short Answer) Why can a value be an outlier within its group but not in the whole dataset (or the other way around)?

**Answer:** A value can be an outlier within its group, but not in the whole dataset because *detection depends on the distribution being used*. 

---

## Section D — Comparing Groups

**23.** (Short Answer) More 3rd-class passengers survived than 2nd-class passengers, but 3rd class had the lower survival rate. How can both be true?

**Answer:** Both can be true because *counts* and *rates* answer different questions.

**24.** (Code Tracing) What does this compute?
```python
titanic.groupby('Sex')['Survived'].mean()
```
**Answer:** This computes *survival rate by sex*.

**25.** (Multiple Choice) In `pd.crosstab(df['class'], df['Sex'], normalize='index')`, what adds up to 100%?
A) each row  B) each column  C) the whole table  D) nothing; it's counts

**Answer:** A) each row 

**26.** (Short Answer) What's the difference between what `pd.crosstab()` and `pivot_table()` compute?

**Answer:** `pd.crosstab()` counts, while `pivot_table()` computes any statistic of a third column, for every combination of two other.

**27.** (Short Answer) Why should a group summary always include the group's size?

**Answer:** A group summary should always inclue the group's size because reliability is based on the size of the data.

**28.** (Short Answer) Cherbourg passengers survived at a higher rate than other ports. Explain how ticket class could be a **confounder** here.

**Answer:** Class affected survival, and class also differed by port, so the port's survival rate is partly a ticket class effect in disguise.

**29.** (Short Answer) What does `observed=True` do in a `groupby` on a categorical column?

**Answer:** In a `groupby` on a categorical column, `observed=True` tells pandas to include only the category levels that appear in the data.

---

## Section E — Relationships and Correlation

**30.** (Short Answer) Why is covariance hard to interpret on its own, and how does correlation fix that?

**Answer:** Covariance is hard to interpret on its own because it depends on the units. Correlation fixes this by standardizing the covariance.

**31.** (Multiple Choice) r = −0.85 means:
A) a weak negative linear relationship  B) a strong negative linear relationship  C) 85% of y is caused by x  D) no relationship

**Answer:** B) a strong negative linear relationship

**32.** (Short Answer) Give two situations where Spearman is a better choice than Pearson.

**Answer:** Two situations where Spearman is the better choice is when the data is *ordinal* or when there are *outliers*.

**33.** (True/False) If r = 0, the two columns have no relationship at all.

**Answer:** False

**34.** (Short Answer) Name three explanations for a correlation besides "A causes B."

**Answer:** Three other explanations for a correlation are *coincidence*, *confounding*, and *reverse causation*.

**35.** (Short Answer) What is Anscombe's quartet, and what lesson does it teach?

**Answer:** Anscombe's quartest is a collection of four datasets that are statistically identical. It teaches that summary statistics alone can be misleading without plotting.

**36.** (Short Answer) In the penguins data, bill length and depth correlate at −0.24 overall but +0.39 to +0.65 within each species. What's this called, and what causes it here?

**Answer:** This is called *Simpson's Paradox*. Here it is caused by pooling "long and shallow" bill groups with "shorter and deeper" bill groups.