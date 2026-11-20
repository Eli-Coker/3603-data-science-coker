# 📝 Quiz: 08 - Visualizing Data

36 questions covering object-oriented Matplotlib, plotting with pandas, Seaborn distributions, Seaborn relationships and categories, and choosing and designing charts. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Matplotlib, Object-Oriented

**1.** (Short Answer) In `fig, ax = plt.subplots()`, what's the difference between `fig` and `ax`?

`Answer:` `fig` represents the whole canvas, whereas `ax` represents one chart.

**2.** (Short Answer) Why does the object-oriented style scale better than `plt.title()`/`plt.xlabel()` calls when a figure has several charts?

`Answer:` Object-oriented style scales better for several charts because it draws on *explicit objects*, meaning you always know which chart you're changing.

**3.** (Code Tracing) How many axes does this create, and how do you reach the bottom-right one?
```python
fig, axes = plt.subplots(2, 3)
```
`Answer:` This creates *6 axes*. You use `axes[1, 2]` to reach the bottom-right one.

**4.** (Short Answer) What does `sharey=True` do, and why does it matter when comparing panels?

`Answer:` `sharey=True` makes all panels use the same y-axis, which matters when comparing panels as it ensures each one uses the same scale.

**5.** (Short Answer) When is a log-scale axis a good idea? What value can't it show?

`Answer:` A log-scale axis is a good idea when data is heavily skewed. It can't show the value 0.

**6.** (Multiple Choice) Which formatter displays `0.25` on an axis as `25%`?
A) `StrMethodFormatter('{x:.0%}')`  B) `PercentFormatter(xmax=1)`  C) `PercentFormatter(xmax=100)`  D) `ax.set(percent=True)`

`Answer:` B) `PercentFormatter(xmax=1)`

**7.** (Short Answer) Why should you call `fig.savefig()` before `plt.show()`, and why `plt.close(fig)` inside a loop?

`Answer:` You should call `fig.savefig()` beforehand because in some environments, calling `plt.show()` also clears the figure. You should use `plt.close(fig)` inside a loop so that figures do not pile up in memory.

**8.** (Short Answer) In `ax.annotate('Peak', xy=(5, 10), xytext=(7, 12), arrowprops=...)`, what do `xy` and `xytext` each mean?

`Answer:` `xy` represents the point being labeled, and `xytext` is where the text sits.

---

## Section B — Plotting with Pandas

**9.** (Short Answer) When pandas plots a DataFrame, what becomes the x-axis, and what becomes each line or set of bars?

`Answer:` The *index* becomes the x-acis, and each *column* becomes a separate line / set of bars.

**10.** (Code Tracing) What kind of chart does this draw, and what are the bar labels?
```python
titanic['Embarked'].value_counts().plot.barh()
```
`Answer:` This draws a *horizontal bar chart*, and the bar labels are the `'Embarked'` codes.

**11.** (Short Answer) You plot a `pivot_table` with classes as the index and sexes as the columns. How do you switch the chart to group by sex instead?

`Answer:` To switch the chart to group by sex, *transpose* it with `.T` (e.g. `ax = survival.T.plot.bar(rot=0, figsize=(7, 4)`)

**12.** (Short Answer) What does a 100% stacked bar chart show, and which `crosstab` argument produces the right table for it?

`Answer:` A 100% stacked bar chart shows the *composition* of each group in the data, where each bar sums up to 100%. The `normalize='index'` argument produces the table for it.

**13.** (Short Answer) What's the difference between wide and long data? Which does pandas `.plot` expect, and which does Seaborn expect?

`Answer:` *Wide data* consists of one column per series, while *long data* consists of one row per observation. Pandas `.plot` expects wide data, whereas Seaborn expects long data.

**14.** (Short Answer) Should you sort the bars of an ordinal category (like ticket class) by value? Why or why not?

`Answer:` You should *not* sort the bars of an ordinal category by value because they consist of a natural and meaningful sequence.

---

## Section C — Seaborn: Distributions

**15.** (Short Answer) What's the difference between an axes-level and a figure-level Seaborn function? Give one example of each.

`Answer:` An **axes-level** function draws on *one `ax`* and returns an `ax` (e.g. `histplot`). A **figure-level** function draws on a *whole new figure* and returns a `FacetGrid` (e.g. `displot`). 

**16.** (Short Answer) What does `hue='species'` do in `sns.histplot()`?

`Answer:` `hue='species'` splits the data by species and colors each group.

**17.** (Multiple Choice) Two groups have 500 and 50 rows. To compare the **shapes** of their distributions, use:
A) `stat='count'`  B) `multiple='stack'`  C) `stat='percent', common_norm=False`  D) `binwidth=1`

`Answer:` C) `stat='percent', common_norm=False`

**18.** (Short Answer) Explain each part of a box plot: the box, the line inside it, the whiskers, and the dots.

`Answer:` The *bottom edge* of the box represents Q1 (25th percentile), and the *top edge* represents Q3 (75th percentile). The *height* of the box represents the IQR. The *line* inside of the box represents median. The *whiskers* represent the smallest and largest values within the fences. The *dots* beyond the fences represent outliers.

**19.** (Short Answer) Name one thing a violin plot shows that a box plot hides, and one thing a strip plot shows that a violin hides.

`Answer:` One thing a violin plot shows that a box plot hides is the *full shape* of the distribution. One thing a strip plot shows that a violin hides is *every individual point*.

**20.** (Short Answer) How do you read a group's median from an ECDF plot?

`Answer:` On an ECDF plot, where a group's curve crosses the defined dotted line is it's median.

**21.** (True/False) A KDE curve always stays within the actual range of the data.

`Answer:` False

**22.** (Short Answer) Why does `showfliers=False` make sense when you draw a strip plot on top of a box plot?

`Answer:` Setting `showfliers=False` for the box plot makes sense in this case because the strip plot already draws every point.

---

## Section D — Seaborn: Relationships and Categories

**23.** (Short Answer) Name two ways to reduce overplotting in a scatter plot.

`Answer:` Two ways include using `alpha` for transparency and using a *log scale* (`yscale='log'`) to spread out crowded points.

**24.** (Short Answer) In the penguins data, one `regplot` line through all the points slopes down, but one line per species slopes up. What's this called, and what's the lesson for fitting trend lines?

`Answer:` This situation is called **Simpson's Paradox**, and it shows that you should separate and color by groups before you fit a line.

**25.** (Short Answer) Why did the four Anscombe datasets get identical lines from `lmplot`?

`Answer:` The points for each Anscombe datasets show the same overall slope and intercept, resulting in identical lines from `lmplot`.

**26.** (Short Answer) What's the difference between `countplot` and `barplot`?

`Answer:` `countplot` shows how many rows are in each category, while `barplot` shows an estimate for each category.

**27.** (Multiple Choice) `sns.barplot(..., errorbar='sd')` draws error bars showing:
A) the 95% confidence interval  B) the standard error  C) one standard deviation of the individual values  D) the IQR

`Answer:` C) one standard deviation of the individual values

**28.** (Short Answer) What does Seaborn's default error bar on a `barplot` represent?

`Answer:` Seaborn's default error bar on a `barplot` represents a *95% confidence interval* for the mean of the data.

**29.** (Short Answer) What does a `pointplot` with crossing or diverging lines tell you?

`Answer:` The crossing/diverging lines in a `pointplot` tell you that the effect of one variable depends on the other (an interaction).

**30.** (Short Answer) Should a correlation heatmap use a diverging or a sequential color map? What about a heatmap of survival rates? Why?

`Answer:` A correlation heatmap should use a *diverging color map*, as they run from -1 to +1 wit a meaningful center at 0. For a heatmap of survival rates, you should use a *sequential color map*, as rates can range from 0 to 1 with no meaningful center value.

---

## Section E — Choosing and Telling

**31.** (Short Answer) Why must bar charts start at zero, when line charts don't have to?

`Answer:` Bar charts must start at zero because a bar's value is shown by it's length; truncating it results in misleading lengths.

**32.** (Short Answer) Name the chart you'd choose for each: (a) the distribution of one numeric column, (b) the mix of categories within each group, (c) the relationship between two numeric columns.

`Answer:` (a) - histogram | (b) - 100% stacked bar chart | (c) - scatter plot

**33.** (Short Answer) What's a palette dictionary, and why use one across a whole report?

`Answer:` A palette dictionary is a mapping between colors and categories. You'd use one across a whole report to keep chart colors consistent.

**34.** (Short Answer) Rewrite this descriptive title as a finding title: "Mean Body Mass by Species."

`Answer:` "Gentoo Penguins Have the Highest Mean Body Mass"

**35.** (True/False) Every bar in a bar chart should have its own distinct color.

`Answer:` False

**36.** (Short Answer) Give two reasons to look at a chart **and** the matching numbers, rather than just one of them.

`Answer:` 1. Charts clearly show patterns that numbers can hide | 2. Matching numbers verify patterns from charts with precision.